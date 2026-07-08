# Impostor 🕵️

Przeglądarkowa gra towarzyska „Impostor" — jeden gracz nie zna hasła i musi blefować.
Statyczny front, **bez backendu**. Działa na dowolnym hostingu statycznego (Vercel, Netlify, GitHub Pages).

- Tryb **jeden telefon** — podajemy urządzenie dalej, każdy widzi tylko swoją rolę. Działa offline.
- Tryb **online** — host tworzy pokój z kodem, reszta dołącza pod swoją nazwą na własnych telefonach; host może wyrzucać graczy. Multiplayer P2P przez [PeerJS](https://peerjs.com) (bez własnego serwera, wymaga internetu).
- ~1400 polskich haseł w 16 kategoriach, losowanie impostora z rzadkimi „szalonymi" rundami (0 / 2 / wszyscy impostorzy), punktacja i tabela wyników.

Cała aplikacja to jeden plik: **`index.html`**.

## Uruchomienie lokalnie

Otwórz `index.html` w przeglądarce (dwuklik) — to wystarczy.
Albo lokalny serwer: `npx serve` lub `python -m http.server`.

## Wdrożenie na Vercel (auto-deploy z GitHub)

### 1. Wrzuć projekt na GitHub

Najprościej w VS Code: **Source Control → „Publish to Branch / Publish to GitHub"**.

Albo z terminala w folderze projektu:

```bash
git init
git add .
git commit -m "Impostor - gra przeglądarkowa"
# utwórz puste repo na github.com/new, potem:
git remote add origin https://github.com/<twoj-login>/impostor.git
git branch -M main
git push -u origin main
```

### 2. Podłącz do Vercel (jednorazowo)

1. Wejdź na https://vercel.com/new
2. Zaloguj się przez GitHub i **zaimportuj** repo `impostor`.
3. Framework Preset: **Other** (to statyczny HTML — żadnej konfiguracji nie trzeba).
4. Kliknij **Deploy**.

Gotowe — dostajesz URL typu `https://impostor-xyz.vercel.app`.

### 3. Auto-deploy

Od tej chwili **każdy `git push` na `main` automatycznie wdraża nową wersję**. Nic więcej nie musisz robić.

## Struktura

```
index.html   # cała gra (HTML + CSS + JS + baza słów)
README.md
.gitignore
```

## Rozbudowa bazy słów

Baza haseł jest wbudowana w `index.html` w zmiennej `WORDS` (na górze sekcji `<script>`).
Aby ją powiększyć, edytujesz `build_words.py` (dostarczony osobno), uruchamiasz `python build_words.py`
i wklejasz nowy `words.json` w miejsce zawartości `WORDS`.
