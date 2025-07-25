<!--- mdformat-toc start --slug=github --->

<!---
!!! README dosyasını düzenliyorsanız, dosyanın tamamını `/docs/` içindeki index.md dosyasına kopyalayın ve ReadTheDocs ile ilgili referansları oradan kaldırın.
--->

<div align="center">

# spotDL v4

**spotDL**, Spotify çalma listelerindeki şarkıları YouTube'da bulur ve indirir - albüm kapağı, şarkı sözleri ve meta verilerle birlikte.

[![MIT Lisansı](https://img.shields.io/github/license/spotdl/spotify-downloader?color=44CC11&style=flat-square)](https://github.com/spotDL/spotify-downloader/blob/master/LICENSE)
[![PyPI sürümü](https://img.shields.io/pypi/pyversions/spotDL?color=%2344CC11&style=flat-square)](https://pypi.org/project/spotdl/)
[![PyPi indirme](https://img.shields.io/pypi/dw/spotDL?label=downloads@pypi&color=344CC11&style=flat-square)](https://pypi.org/project/spotdl/)
![Katkıda Bulunanlar](https://img.shields.io/github/contributors/spotDL/spotify-downloader?style=flat-square)
[![Discord](https://img.shields.io/discord/771628785447337985?label=discord&logo=discord&style=flat-square)](https://discord.gg/xCa23pwJWY)

> spotDL: En hızlı, en kolay ve en doğru komut satırı müzik indiricisi.
</div>

______________________________________________________________________
**[ReadTheDocs üzerinden dokümantasyonu okuyun!](https://spotdl.readthedocs.io)**
______________________________________________________________________

## Kurulum

Daha fazla detay için [Kurulum Rehberi](https://spotdl.rtfd.io/en/latest/installation/) adresine bakabilirsiniz.

### Python (Önerilen Yöntem)
  - _spotDL_’yi `pip install spotdl` komutu ile kurabilirsiniz.
  - spotDL’i güncellemek için `pip install --upgrade spotdl` komutunu kullanın.

  > Bazı sistemlerde `pip` yerine `pip3` kullanmanız gerekebilir.

<details>
    <summary style="font-size:1.25em"><strong>Diğer seçenekler</strong></summary>

- Hazır derlenmiş uygulama
  - En son sürümü [Releases Tab](https://github.com/spotDL/spotify-downloader/releases) üzerinden indirebilirsiniz.
- Termux üzerinde
  - `curl -L https://raw.githubusercontent.com/spotDL/spotify-downloader/master/scripts/termux.sh | sh`
- Arch
  - spotDL için bir [Arch User Repository (AUR) paketi](https://aur.archlinux.org/packages/spotdl/) mevcuttur.
- Docker
  - İmajı oluşturun:
    ```bash
    docker build -t spotdl .
    ```
  - spotDL parametreleriyle konteyneri başlatın (aşağıdaki bölüme bakınız). Şarkı dosyalarına erişmek için bir klasör eşlemesi oluşturmalısınız.
    ```bash
    docker run --rm -v $(pwd):/music spotdl download [parcaUrl]
    ```
- Kaynaktan derlemek
	```bash
	git clone https://github.com/spotDL/spotify-downloader && cd spotify-downloader
	pip install poetry
	poetry install
	poetry run python3 scripts/build.py
	```
	`spotify-downloader/dist/` klasöründe bir uygulama oluşturulur.

</details>

### FFmpeg Kurulumu

spotDL için FFmpeg gereklidir. Yalnızca spotDL için FFmpeg kullanacaksanız, FFmpeg’i doğrudan spotDL kurulum dizinine yükleyebilirsiniz:
`spotdl --download-ffmpeg`

Yukarıdaki seçeneği öneriyoruz, ancak FFmpeg’i sistem genelinde kurmak isterseniz aşağıdaki talimatları izleyin:

- [Windows Eğitimi](https://windowsloop.com/install-ffmpeg-windows-10/)
- OSX - `brew install ffmpeg`
- Linux - `sudo apt install ffmpeg` veya dağıtımınızın paket yöneticisini kullanın

## Kullanım

SpotDL’i seçenekler olmadan kullanmak için:
```sh
spotdl [url’ler]
```
SpotDL’i bir paket olarak da çalıştırabilirsiniz:
```sh
python -m spotdl [url’ler]
```

Genel kullanım:
```sh
spotdl [işlem] [seçenekler] SORGULAMA
```

spotDL’in farklı **işlemleri** vardır. *Varsayılan* işlem `download`’dır; bu sadece şarkıları YouTube’dan indirir ve meta verileri gömer.

**Sorgu**, genellikle bir Spotify URL listesi olur, ancak **sync** gibi bazı işlemler için yalnızca bir bağlantı veya dosya gereklidir.
Tüm **seçenekler** listesini görmek için ```spotdl -h``` komutunu kullanın.

<details>
<summary style="font-size:1em"><strong>Desteklenen işlemler</strong></summary>

- `save`: Sadece Spotify'dan meta verileri kaydeder, herhangi bir indirme yapmaz.
    - Kullanım:
        `spotdl save [sorgu] --save-file {dosyaAdi}.spotdl`

- `web`: Komut satırı yerine bir web arayüzü başlatır. Ancak, sınırlı özelliklere sahiptir ve sadece tekli şarkı indirmeyi destekler.

- `url`: Sorgudaki her şarkı için doğrudan indirme linkini alır.
    - Kullanım:
        `spotdl url [sorgu]`

- `sync`: Dizinleri günceller. Dizin ile çalma listesinin mevcut durumunu karşılaştırır. Yeni eklenen şarkılar indirilir, kaldırılan şarkılar silinir. Diğer şarkılar indirilmeyecek veya silinmeyecektir.
    - Kullanım:
        `spotdl sync [sorgu] --save-file {dosyaAdi}.spotdl`

        Bu işlem yeni bir **sync** dosyası oluşturur, dizini daha sonra güncellemek için:
        `spotdl sync {dosyaAdi}.spotdl`

- `meta`: Sağlanan şarkı dosyalarının meta verilerini günceller.

</details>

## Müzik Kaynağı ve Ses Kalitesi

spotDL, müzik indirme için YouTube’u kaynak olarak kullanır. Bu yöntem, Spotify’dan müzik indirme ile ilgili sorunların önüne geçmek için tercih edilir.

> **Not**
> Kullanıcılar kendi eylemlerinden ve olası hukuki sonuçlardan sorumludur. SpotDL, telif hakkı olan materyalin izinsiz indirilmesini desteklemez ve kullanıcıların eylemlerinden sorumlu değildir.

### Ses Kalitesi

spotDL, müzikleri YouTube’dan indirir ve her zaman mümkün olan en yüksek bitrate’i indirmeye çalışır; normal kullanıcılar için 128 kbps, YouTube Music premium kullanıcıları için ise 256 kbps.

Daha fazla bilgi için [Ses Formatları](docs/usage.md#audio-formats-and-quality) sayfasına göz atın.

## Katkıda Bulunma

Katkıda bulunmak ister misiniz? [CONTRIBUTING.md](docs/CONTRIBUTING.md) dosyasına göz atarak katkı kaynaklarına ve geliştirme ortamının nasıl kurulacağına dair rehbere ulaşabilirsiniz.

### Harika topluluğumuza kod katkıcısı olarak katılın ve gelişimi hızlandırın!

<br><br>
<a href="https://github.com/spotDL/spotify-downloader/graphs/contributors">
  <img class="dark-light" src="https://contrib.rocks/image?repo=spotDL/spotify-downloader&anon=0&columns=25&max=100&r=true" />
</a>

## Lisans

Bu proje [MIT](/LICENSE) Lisansı ile lisanslanmıştır.

## Çeviri

Bu proje Burak Can Öğüt tarafından çevrilmiştir. 
