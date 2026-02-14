# Audit repozitaru -- Citliva data, .gitignore, artefakty, README

**Datum:** 2026-02-14
**Rozsah:** Vsechny verejne repozitare Slapeto23

---

## 1. Prehled repozitaru

| # | Repozitar | Citliva data | .gitignore | Artefakty | README CZ |
|---|-----------|-------------|------------|-----------|-----------|
| 1 | HlidacStatu-InsolvencniRejstrik | Cisty | OK (331 radku) | Zadne | Uz existuje |
| 2 | tanstack-template | Cisty | Vylepseno | Zadne | Pridano (README.cs.md) |
| 3 | Slapeto23 | 2 nalezy -- OPRAVENO | Vylepseno | Zadne | Pridano (README.md) |
| 4 | packaging.python.org | Cisty | OK | Zadne | Pridano (README.cs.md) |
| 5 | servers | Cisty | Vynikajici (301 radku) | Zadne | Pridano (README.cs.md) |
| 6 | pi-explorer | Cisty | OK | Zadne | Pridano (README.cs.md) |
| 7 | nextjs-ai-chatbot | Neexistuje | -- | -- | -- |
| 8 | desktop-tutorial | Neexistuje | -- | -- | -- |

---

## 2. Opravene bezpecnostni nalezy (Slapeto23/Slapeto23)

### Nalez 1: Hardcoded JWT secret -- OPRAVENO

- **Soubor:** `src/auth.js`, radek 6
- **Puvodni kod:** `const DEFAULT_SECRET = 'default-secret-change-in-production';`
- **Oprava:** Odstranen vychozi secret. Konstruktor nyni vyzaduje `secret` jako povinny parametr a vyhodi chybu, pokud neni zadan.
- **Testy:** Vsech 69 testu prochazi po uprave.

### Nalez 2: Interni proxy URL -- OPRAVENO

- **Soubor:** `package.json`, pole `repository.url`
- **Puvodni URL:** `http://local_proxy@127.0.0.1:58388/git/Slapeto23/Slapeto23`
- **Oprava:** Nahrazeno standardni GitHub URL: `https://github.com/Slapeto23/Slapeto23.git`

---

## 3. Audit .gitignore

### HlidacStatu-InsolvencniRejstrik -- OK
Komplexni .gitignore pro Visual Studio (331 radku). Pokryva vsechny build artefakty, NuGet balicky, IDE soubory.

### tanstack-template -- VYLEPSENO
Puvodni .gitignore obsahoval jen 8 zaznamu. Doplneny:
- `.env.local`, `.env.*.local` (lokalni env soubory)
- `*.log`, `npm-debug.log*`, `yarn-debug.log*` (logy)
- `.idea/`, `*.swp`, `*.swo`, `*~` (IDE soubory)
- `*.tsbuildinfo` (TypeScript cache)
- `coverage/` (testovaci pokryti)

### Slapeto23 -- VYLEPSENO
Puvodni .gitignore obsahoval jen `node_modules/`. Doplneny:
- `dist/`, `build/`, `coverage/` (build artefakty)
- `.env`, `.env.local`, `.env.*.local` (env soubory)
- `*.log`, `npm-debug.log*` (logy)
- `.DS_Store`, `.idea/`, `.vscode/`, `*.swp` (system/IDE)

### packaging.python.org -- OK
Minimalni ale dostatecny pro dokumentacni projekt (Sphinx). Pokryva `build/`, `*.pyc`, `__pycache__`, `.nox`.

### servers -- VYNIKAJICI
Komplexni .gitignore (301 radku) pokryvajici JS i Python ekosystem, env soubory, credentials, IDE soubory.

### pi-explorer -- OK
Dostatecny pro React projekt. Pokryva `node_modules`, `build`, `coverage`, `.env`, `.DS_Store`, logy.

---

## 4. Audit commitnutych artefaktu

Zadny repozitar neobsahuje commitnute problematicke soubory:
- Zadne `node_modules/`
- Zadne `.env` soubory s realnimi hodnotami
- Zadne build artefakty (`dist/`, `build/`, `bin/`, `obj/`)
- Zadne `coverage/` slozky
- Zadne `__pycache__/` nebo `*.pyc`
- Zadne zkompiliovane binarne soubory

---

## 5. Ceske README

| Repozitar | Soubor | Popis |
|-----------|--------|-------|
| HlidacStatu-InsolvencniRejstrik | `README.md` | Jiz existovalo v cestine |
| Slapeto23 | `README.md` | Vytvoreno -- popis autentizacniho modulu |
| tanstack-template | `README.cs.md` | Vytvoreno -- popis chatovaci sablony |
| packaging.python.org | `README.cs.md` | Vytvoreno -- popis prirucky pro balickovani |
| servers | `README.cs.md` | Vytvoreno -- popis MCP serveru |
| pi-explorer | `README.cs.md` | Vytvoreno -- popis prohlizece bloku |

---

## 6. Aplikace zmen

Zmeny pro ostatni repozitare jsou ulozene jako patch soubory ve slozce `patches/`:

```bash
# Slapeto23/Slapeto23 (bezpecnostni opravy + .gitignore + README)
cd ~/Slapeto23 && git am < patches/Slapeto23.patch

# Slapeto23/tanstack-template (.gitignore + README)
cd ~/tanstack-template && git am < patches/tanstack-template.patch

# Slapeto23/packaging.python.org (README)
cd ~/packaging.python.org && git am < patches/packaging.python.org.patch

# Slapeto23/servers (README)
cd ~/servers && git am < patches/servers.patch

# Slapeto23/pi-explorer (README)
cd ~/pi-explorer && git am < patches/pi-explorer.patch
```
