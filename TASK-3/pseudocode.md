IF secim = 1 THEN
  // Randevu Sistemi
  poliklinikler ← getPoliklinikListesi()
  DISPLAY poliklinikler

  DISPLAY "Lütfen bir poliklinik seçiniz:"
  INPUT secilenPoliklinik

  doktorlar ← getDoktorlar(secilenPoliklinik)
  DISPLAY doktorlar

  DISPLAY "Lütfen bir doktor seçiniz:"
  INPUT secilenDoktor

  uygunSaatler ← getUygunSaatler(secilenDoktor)
  DISPLAY uygunSaatler

  DISPLAY "Lütfen bir saat seçiniz:"
  INPUT secilenSaat

  DISPLAY "Randevunuz: " + secilenPoliklinik + ", " + secilenDoktor + ", " + secilenSaat
  DISPLAY "Onaylıyor musunuz? (E/H)"
  INPUT onay

  IF onay = "E" THEN
    randevuID ← kaydetRandevu(tcKimlikNo, secilenPoliklinik, secilenDoktor, secilenSaat)
    mesaj ← "Randevunuz başarıyla oluşturuldu. Randevu ID: " + randevuID
    DISPLAY mesaj
    sendSMS(tcKimlikNo, mesaj)
  ELSE
    DISPLAY "Randevu iptal edildi."
  ENDIF

ELSE IF secim = 2 THEN
  // Tahlil Sonucu Sistemi
  tahlilListesi ← getTahlilKayitlari(tcKimlikNo)

  IF tahlilListesi IS EMPTY THEN
    DISPLAY "Sistemde kayıtlı tahlil bulunmamaktadır."
  ELSE
    FOR EACH tahlil IN tahlilListesi DO
      IF tahlil.sonucHazir = TRUE THEN
        DISPLAY "Tahlil: " + tahlil.ad + " - Sonuç hazır."
        DISPLAY "Sonucu görüntülemek ister misiniz? (E/H)"
        INPUT cevap

        IF cevap = "E" THEN
          DISPLAY "Sonuç: " + tahlil.sonuc
          DISPLAY "PDF olarak indirmek ister misiniz? (E/H)"
          INPUT pdfCevap

          IF pdfCevap = "E" THEN
            pdfDosya ← generatePDF(tahlil)
            DISPLAY "PDF dosyası indiriliyor: " + pdfDosya
          ENDIF
        ENDIF
      ELSE
        DISPLAY "Tahlil: " + tahlil.ad + " - Sonuç henüz hazır değil."
      ENDIF
    ENDFOR
  ENDIF

ELSE IF secim = 3 THEN
  DISPLAY "Sistemden çıkılıyor. Sağlıklı günler!"
  EXIT

ELSE
  DISPLAY "Geçersiz seçim. Lütfen 1-3 arasında bir değer giriniz."
ENDIF
