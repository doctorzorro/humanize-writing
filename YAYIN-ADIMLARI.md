# GitHub'a Yükleme Adımları (humanize-writing)

Bu klasör push'a hazır: README.md + LICENSE + SKILL.md. gh CLI kurulu DEĞİL, o yüzden iki yol var.

## Yol A — GitHub web arayüzü (en kolay, kurulum yok)

1. github.com → **New repository**
2. Repo adı: `humanize-writing` · **Public** · README/LICENSE **ekleme** (bizde var)
3. "uploading an existing file" bağlantısına tıkla
4. Bu klasördeki 3 dosyayı sürükle-bırak: `README.md`, `LICENSE`, `SKILL.md`
5. Commit → bitti

## Yol B — git komut satırı (gh gerekmez, sadece git)

```bash
cd "Desktop/pazarlama-lansman/github-humanize-writing"
git init
git add .
git commit -m "humanize-writing: anti-slop Claude Code skill"
git branch -M main
# GitHub'da BOŞ repo aç (README'siz), sonra:
git remote add origin https://github.com/<KULLANICI-ADIN>/humanize-writing.git
git push -u origin main
```

## Yükledikten sonra (backlink + keşif için)

- **About** kısmına (repo sağ üst): kısa açıklama + `hekimsoft.com` link koy
- **Topics** ekle: `claude`, `claude-code`, `ai-writing`, `content`, `anti-slop`, `llm`
- README zaten hekimsoft.com'a link veriyor — **softlink stratejisi** çalışıyor
- Repo linkini Gumroad'daki ücretsiz Humanize Writing ürününün açıklamasına da koy (çapraz bağ)

## Neden GitHub?

Satış için değil — **keşif + geri-bağlantı.** Geliştiriciler "claude code skill" ararken bulur, yıldızlar, README'den siteye gider. Ücretsiz olduğu için indirme engeli yok; huninin en geniş ağzı burası.
