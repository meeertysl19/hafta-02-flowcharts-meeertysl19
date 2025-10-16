PIN_HAK = 3
DOGRU_PIN = 1234
BAKIYE = 5000
GUNLUK_LIMIT = 2000
GUNLUK_CEKILEN = 0

DONGU PIN_HAK > 0 ISE
    YAZ "Lütfen PIN kodunuzu giriniz:"
    OKU GIRILEN_PIN

    EGER GIRILEN_PIN = DOGRU_PIN ISE
        YAZ "PIN doğrulandı."
        CIK
    DEGILSE
        PIN_HAK = PIN_HAK - 1
        EGER PIN_HAK > 0 ISE
            YAZ "Yanlış PIN. Kalan deneme hakkınız: ", PIN_HAK
        DEGILSE
            YAZ "3 kez yanlış PIN girildi. Kart bloke edildi."
            DUR
        BITIR
    BITIR
BITIR

DONGU TRUE ISE
    YAZ "Çekmek istediğiniz tutarı giriniz (20 TL katı):"
    OKU TUTAR

    EGER TUTAR MOD 20 ≠ 0 ISE
        YAZ "Lütfen 20 TL'nin katı bir tutar giriniz."
        DEVAM
    BITIR

    EGER TUTAR > BAKIYE ISE
        YAZ "Yetersiz bakiye. Mevcut bakiye: ", BAKIYE
        DEVAM
    BITIR

    EGER GUNLUK_CEKILEN + TUTAR > GUNLUK_LIMIT ISE
        YAZ "Günlük limit aşıldı. Kalan limit: ", GUNLUK_LIMIT - GUNLUK_CEKILEN
        DEVAM
    BITIR

    BAKIYE = BAKIYE - TUTAR
    GUNLUK_CEKILEN = GUNLUK_CEKILEN + TUTAR
    YAZ "İşlem başarılı. Yeni bakiye: ", BAKIYE

    YAZ "Başka bir işlem yapmak ister misiniz? (E/H):"
    OKU CEVAP

    EGER CEVAP = "H" ISE
        YAZ "İyi günler!"
        DUR
    BITIR
BITIR
