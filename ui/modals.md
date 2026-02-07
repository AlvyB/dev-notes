# Modalų kūrimo taisyklės

## 1. Modalą laikyk UI komponentu, ne „page feature“
- Modalas turi būti atskiras komponentas (`Modal`) su aiškiu API.
- Visas vidinis HTML / JS turi būti vienoje vietoje.
- Nekeičiame 20 failų tam pačiam elgesiui.

---

## 2. Modalas turi turėti vieną „open“ būseną
- Vienas boolean (`open`, `isOpen`).
- Nevaldyti per „render if open“, jei modalas turi formą ar state.

---

## 3. Uždarymas privalo veikti 3 būdais
Visada turi veikti:
- `ESC`
- Backdrop click
- Close mygtukas (X)

Visi trys privalo kviesti **tą pačią** `close()` logiką.

---

## 4. Nesunaikink DOM, jei viduje yra state
Jei modale yra:
- inputai
- formos
- editoriai

Tada:
- ❌ nenaudoti `@if`, conditional render, unmount
- ✅ naudoti `x-show`, `hidden`, `dialog open=false`

Kodėl: kitaip prarandami duomenys, focus ir widget būsenos.

> Išimtis: paprasti confirm modalai be state – galima unmount.

---

## 5. Privalomas Focus Trap
Kai modalas atidarytas:
- `TAB` neturi išeiti už modal’o ribų.
- Fokusas turi patekti į modalą (pirmas input arba container).

Be to UX ir accessibility bus blogi.

---

## 6. Privalomas Scroll Lock
Kai modalas `open`:
- background neturi scrollintis (ypač mobile).

Kai modalas `close`:
- scroll turi būti grąžintas.

> Dažniausias bugas be scroll lock: „modalas atidarytas, bet puslapis juda“.

---

## 7. Modalas turi būti virš visko (stacking)
- Overlay ir modal content turi turėti standartinius `z-index`.
- Vengti renderinimo konteineryje su `overflow: hidden`.

Jei reikia – renderinti į „root“ (portal / teleport).

---

## 8. Modalas turi būti ARIA korektiškas
Minimalūs reikalavimai:
- `role="dialog"`
- `aria-modal="true"`
- `aria-labelledby` (title)
- `aria-describedby` (subtitle / description, jei yra)

Svarbu accessibility ir screen reader’iams.

---

## 9. Modalas turi aiškų layout contract
- Header (title / subtitle) – optional
- Body (content / slot) – **privalomas**
- Footer / actions – optional

Tai garantuoja vizualinį nuoseklumą.

---

## 10. Modalas turi „clean lifecycle“
Atidarant:
- `open()`
- (jei reikia) užkrauti duomenis
- focus į modalą arba pirmą input

Uždarant:
- `close()`
- grąžinti focus į elementą, kuris atidarė modalą

---

## 11. „Heavy widgets“ taisyklė
Jei modale yra:
- editoriai
- žemėlapiai
- grafikai

Tada:
- inicijuoti tik atidarius
- sunaikinti uždarius

Kitaip atsiras memory leak’ai ir lagas.

---

## 12. Vienas modalas – viena atsakomybė
- Nekišti kelių skirtingų flow į vieną modalą su `if`’ais.
- Jei reikia kelių flow – naudoti:
  - kelis modalus
  - arba wizard / stepper

---

## Greitas patikrinimo testas
Modalas padarytas teisingai, jei:

- TAB nelenda į background ✅  
- ESC visada uždaro ✅  
- Backdrop click uždaro (jei ne persistent) ✅  
- Background nescrollina ✅  
- Formos duomenys nedingsta (jei turi likti) ✅  
- Modalas nėra „nukirptas“ dėl `overflow` ✅  
:)