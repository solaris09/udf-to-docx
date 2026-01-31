# UDF → DOCX Dönüştürücü 🔧

Bu küçük araç, belirttiğiniz kök klasör altında (alt klasörler dahil) bulunan tüm `.udf` dosyalarını `.docx` (Word) dosyalarına dönüştürür.

Özellikler
- Öncelikle `pandoc` ile dönüştürmeye çalışır (metin / markdown için en iyi sonuç).
- Pandoc başarısız olursa `LibreOffice` headless modunda dönüştürmeyi dener.
- Her iki yöntem de tutmazsa dosyayı metin olarak okuyup `python-docx` ile basit bir `.docx` oluşturmaya düşer.
- Aynı isimle `.docx` olarak kaydeder (varsayılan davranış: özgün dosyanın yanına). İsterseniz `--out-dir` ile başka bir köke yazdırabilirsiniz.

Kurulum (macOS)

1) Homebrew varsa:

```bash
brew install pandoc
brew install --cask libreoffice
pip3 install python-docx
```

Kullanım

```bash
# Çalıştırılabilir yapmak (isteğe bağlı)
chmod +x convert_udf_to_docx.py

# UYAP-TOOL içindeki .udf dosyalarını aynı yerlerine .docx olarak dönüştür
python3 convert_udf_to_docx.py /Users/cemalhekimoglu/Downloads/UYAP-TOOL

# Alternatif: çıktıları ayrı bir klasöre almak
python3 convert_udf_to_docx.py /Users/cemalhekimoglu/Downloads/UYAP-TOOL --out-dir /Users/cemalhekimoglu/Downloads/UYAP-TOOL-docx

# Varolan .docx dosyalarını üzerine yazmak isterseniz
python3 convert_udf_to_docx.py /Users/cemalhekimoglu/Downloads/UYAP-TOOL --overwrite

# Neler yapılacağını görmek için dry-run
python3 convert_udf_to_docx.py /Users/cemalhekimoglu/Downloads/UYAP-TOOL --dry-run

# Daha ayrıntılı çıktı isterseniz
python3 convert_udf_to_docx.py /Users/cemalhekimoglu/Downloads/UYAP-TOOL -v
```



İhtiyacınız olursa script'i doğrudan sizin klasörde çalıştırıp sonuçları raporlayabilirim (izninizi ve bilgisayarınızda gerekli araçların yüklü olup olmadığını bildirin).

---

## Kurulum (detaylı)

Aşağıda macOS için adım adım kurulum ve çalışma talimatı verilmiştir. Linux üzerinde çalıştıracaksanız paket yöneticinizin (apt/dnf/pacman vb.) eşdeğerlerini kullanın.

1) Homebrew yoksa yükleyin (isteğe bağlı, ama önerilir):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2) Gerekli paketleri yükleyin:

```bash
brew install pandoc
brew install --cask libreoffice
```

3) Proje klasörüne geçin ve Python sanal ortamı oluşturup etkinleştirin:

```bash
cd /path/to/udf-to-docx
python3 -m venv .venv
source .venv/bin/activate
```

4) Gereksinimleri yükleyin:

```bash
pip install -r requirements.txt
```

5) (Opsiyonel) `gh` CLI ile GitHub üzerinde public repo oluşturmak isterseniz (önerilir):

```bash
# gh CLI kurulu ve oturum açılmış olmalı
gh repo create udf-to-docx --public --source=. --remote=origin --push --confirm
```

6) Dry-run ile kontrol edin:

```bash
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL --dry-run -v
```

7) Gerçek çalıştırma:

```bash
python3 convert_udf_to_docx.py /path/to/UYAP-TOOL -v
```

## Lisans ve Yazar

- License: MIT
- Author: **cemal hekimoğlu**
