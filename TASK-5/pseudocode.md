BAŞLA

SistemDurumu ← "AKTİF"

WHILE SistemDurumu = "AKTİF" DO // Sensör verilerini oku Hareket ← HareketSensörü.OKU() KapıDurumu ← KapıSensörü.OKU() CamDurumu ← CamSensörü.OKU() Duman ← DumanSensörü.OKU() SuBaskını ← SuSensörü.OKU()

// Tehdit algılama
EĞER Hareket = "VAR" VE EvDurumu = "BOŞ" İSE
    Tehdit ← "İzinsiz giriş"
EĞER KapıDurumu = "AÇIK" VE Zaman = "Gece" İSE
    Tehdit ← "Şüpheli kapı açılması"
EĞER CamDurumu = "KIRIK" İSE
    Tehdit ← "Cam kırılması"
EĞER Duman = "YÜKSEK" İSE
    Tehdit ← "Yangın riski"
EĞER SuBaskını = "VAR" İSE
    Tehdit ← "Su baskını"

// Alarm verme
EĞER Tehdit TANIMLI İSE
    Alarm.SESLI()
    Alarm.ISIKLI()
    Kamera.KAYDET()
    
    // Bildirim gönder
    Bildirim.GÖNDER("Tehdit algılandı: " + Tehdit)
    Log.KAYDET(Tehdit + " - " + Zaman + " - " + Konum)
DEĞİLSE
    Sistem.LOG("Durum normal - " + Zaman)
BİTİR

BEKLE(5 saniye) // Sistem kaynaklarını korumak için kısa bekleme
BİTİR

DUR
