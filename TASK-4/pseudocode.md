BAŞLA

ÖğrenciDersListesi ← öğrenci tarafından seçilen dersler ToplamKredi ← 0 HataMesajları ← boş liste

HER ders IN ÖğrenciDersListesi İÇİN EĞER ders.kontenjan < ders.kayıtlı_öğrenci_sayısı İSE HataMesajları.EKLE("Kontenjan dolu: " + ders.ad) DEĞİLSE EĞER ders.önkoşul VARSA HER koşul IN ders.önkoşul İÇİN EĞER öğrenci.transkript KOŞULU GEÇMEDİ İSE HataMesajları.EKLE("Ön koşul eksik: " + ders.ad) BİTİR BİTİR BİTİR

    HER diğer_ders IN ÖğrenciDersListesi İÇİN
        EĞER ders ≠ diğer_ders İSE
            EĞER ders.zaman ÇAKIŞIYORSA diğer_ders.zaman İLE
                HataMesajları.EKLE("Zaman çakışması: " + ders.ad + " ↔ " + diğer_ders.ad)
            BİTİR
        BİTİR
    BİTİR

    ToplamKredi ← ToplamKredi + ders.kredi
BİTİR
BİTİR

EĞER ToplamKredi > öğrenci.kredi_limiti İSE HataMesajları.EKLE("Kredi limiti aşıldı: " + ToplamKredi + " kredi") BİTİR

EĞER HataMesajları BOŞSA EĞER danışman.onayladı İSE YAZ "Ders kaydı başarıyla tamamlandı." DEĞİLSE YAZ "Danışman onayı bekleniyor." BİTİR DEĞİLSE HER hata IN HataMesajları İÇİN YAZ hata BİTİR YAZ "Ders kaydı başarısız. Lütfen hataları düzeltin." BİTİR

DUR
