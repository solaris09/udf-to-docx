# UDF → DOCX Dönüştürücü

Basit ve güvenilir bir araç: belirtilen kök klasörün altındaki tüm `.udf` dosyalarını `.docx` (Microsoft Word) formatına dönüştürür.

Özellikler
- Dönüşüm için şu sırayı dener: `pandoc` → `LibreOffice (headless)` → içerik çıkarma ve `python-docx` ile yazma (fallback).
- Varsayılan olarak özgün dosyanın yanına aynı isimle `.docx` oluşturur. `--out-dir` ile çıktı kökünü değiştirebilirsiniz.
- `--dry-run` ile hangi dosyaların dönüştürüleceğini görebilirsiniz; `-v` ayrıntılı çıktı sağlar.

Kurulum (macOS)

Gerekli araçlar: `pandoc`, `LibreOffice` ve Python (`python3`). Homebrew kullanıyorsanız:

```bash
brew install pandoc
brew install --cask libreoffice
```

Proje bağımlılıklarını yükleyin:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Kullanım

```bash
# (isteğe bağlı) çalıştırılabilir yapma
chmod +x convert_udf_to_docx.py

# Klasördeki .udf dosyalarını aynı dizinlere .docx olarak dönüştür
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL

# Çıktıları ayrı bir klasöre almak
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL --out-dir /path/to/output

# Varolan .docx dosyalarını üzerine yazmak
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL --overwrite

# Dry-run (değişiklik yapmaz)
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL --dry-run -v

# Daha ayrıntılı çıktı için
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL -v
```

Notlar
- Araç, farklı `.udf` varyantları için birkaç dönüşüm stratejisi uygular; çoğu durumda başarılı sonuç alınır.

Yazar
- cemal hekimoğlu

Lisans
- MIT — detaylar LICENSE dosyasında.

---

## Detaylı Kurulum (opsiyonel)

Linux kullanıyorsanız paket yöneticinize göre `pandoc` ve `libreoffice` paketlerini yükleyin.

1) Homebrew yüklü değilse (macOS) isterseniz yükleyin:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2) Gerekli paketleri yükleyin:

```bash
brew install pandoc
brew install --cask libreoffice
```

3) Sanal ortam oluşturup bağımlılıkları yükleyin:

```bash
cd /path/to/udf-to-docx
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

4) Repo oluşturma (opsiyonel, `gh` CLI ile):

```bash
# gh CLI kurulu ve oturum açılmış olmalı
gh repo create udf-to-docx --public --source=. --remote=origin --push --confirm
```

5) Test için dry-run çalıştırın:

```bash
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL --dry-run -v
```

6) Gerçek dönüşüm:

```bash
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL -v
```
