BASLA E-TICARET_SISTEMI

  BASLA KULLANICI_GIRISI
    KULLANICI_GIRDI_MI ← FALSE
    EGER kullanici_adi VE sifre DOGRU ISE
      KULLANICI_GIRDI_MI ← TRUE
    DEGILSE
      MESAJ ← "Giriş bilgileri hatalı"
    BITIR
  BITIR

  BASLA URUN_EKLEME
    DONGU kullanici_urun_secene kadar
      SECILEN_URUN ← kullanici_secimi
      BASLA STOK_KONTROL
        EGER SECILEN_URUN.stok > 0 ISE
          SEPETE_EKLE(SECILEN_URUN)
        DEGILSE
          MESAJ ← "Ürün stokta yok"
        BITIR
      BITIR
    DONGU_SONU
  BITIR

  BASLA SEPET_YONETIMI
    DONGU kullanici_sepeti_duzenle kadar
      GOSTER_SEPET()
      SECIM ← kullanici_secimi
      EGER SECIM = "sil" ISE
        URUN_SIL()
      EGER SECIM = "adet_degistir" ISE
        ADET_GUNCELLE()
    DONGU_SONU
  BITIR

  BASLA INDIRIM_KODU_KONTROL
    EGER kullanici_indirim_kodu_girdi ISE
      EGER KOD_GECERLI(kullanici_kodu) ISE
        INDIRIM_UYGULA()
      DEGILSE
        MESAJ ← "Kod geçersiz"
      BITIR
    BITIR
  BITIR

  BASLA KARGO_HESAPLAMA
    ADRES ← kullanici_adresi
    KARGO_UCRETI ← HESAPLA_KARGO(ADRES)
    EGER SEPET_TUTARI > UCRETSIZ_KARGO_ESIGI ISE
      KARGO_UCRETI ← 0
    BITIR
  BITIR

  BASLA ODEME_ASAMALARI
    GOSTER_SIPARIS_OZETI()
    ODEME_YONTEMI ← kullanici_secimi
    EGER ODEME_YONTEMI = "kredi_karti" ISE
      BASLA KART_BILGISI_KONTROL
        EGER KART_GECERLI(kart_bilgileri) ISE
          ODEME_ONAYLA()
        DEGILSE
          MESAJ ← "Kart bilgileri geçersiz"
        BITIR
      BITIR
    EGER ODEME_YONTEMI = "kapida_odeme" ISE
      ODEME_ONAYLA()
    BITIR
  BITIR

  BASLA SIPARIS_TAMAMLAMA
    SIPARIS_OLUSTUR()
    MESAJ ← "Siparişiniz başarıyla oluşturuldu"
  BITIR

BITIR E-TICARET_SISTEMI
