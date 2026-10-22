# Dot Maze

Siyah noktayı labirentin çıkışına ulaştır. Her bölüm bir öncekinden büyük ve zor.
Tarayıcıda ve telefonda oynanır — kurulum yok, bağımlılık yok, tek dosya.

**▶ Oyna:** https://mryesiller.github.io/dot-maze/

## Özellikler

- **Süre ve adım takibi** — her bölümde canlı süre ve adım sayacı; bölüm sonunda "en az adım" ve kişisel rekorlarınla karşılaştırma ("YENİ REKOR" işareti).
- **Yıldız derecesi** — adım sayın, BFS ile bulunan en kısa yola göre 1–3 yıldız verir (kusursuz tur = ★★★).
- **İstatistik paneli** — tamamlanan bölüm, toplam yıldız, toplam adım, toplam süre ve bölüm bazında en iyi sonuçlar. Panel açıkken ve sekme arka plandayken sayaç durur.
- **Bölüm sistemi** — ızgara 5×5'ten başlayıp 40×40'a kadar büyür; ilerledikçe algoritma çeşitlenir (backtracker → sidewinder → prim/kruskal → wilson) ve döngüler (braiding) eklenir.
- **Deterministik bölümler** — her bölüm numarası sabit bir seed'den üretilir; herkes aynı bölümü görür.
- **İlerleme cihazda saklanır** (`localStorage`) — kaldığın bölümden devam edersin.
- **Web + mobil** — klavye (ok tuşları / WASD), ekran D-pad'i ve kaydırma (swipe). Büyük labirentlerde kamera noktayı takip eder. Açık/koyu tema, `prefers-reduced-motion` desteği.

## Kontroller

| Eylem | Masaüstü | Mobil |
|---|---|---|
| Hareket | Ok tuşları / WASD | Kaydır veya D-pad |
| Bölümü yeniden başlat | `R` | ↻ düğmesi |
| İstatistikler | `Esc` | ▮▮▮ düğmesi |
| Sıradaki bölüm | `Enter` / `Boşluk` | "Sıradaki" düğmesi |

## Yerelde çalıştırma

Derleme adımı yok. `index.html` dosyasını tarayıcıda açman yeterli ya da:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Yapı

Tüm oyun `index.html` içindedir:

- **Üretim**: seed'li PRNG (`xmur3` + `mulberry32`), 5 labirent algoritması, braiding, BFS çözücü.
- **Oyun**: sabit ızgara hareketi, çarpışma, girdi kuyruğu, kamera, yıldız/rekor hesabı, kayıt.
- **Render**: labirent bir kez offscreen canvas'a çizilir; her karede yalnızca kamera + oyuncu çizilir.

Kayıt anahtarı `dotmaze.v1`. Konsoldan `window.__dm` ile durum incelenebilir.

## Lisans

[MIT](LICENSE)
