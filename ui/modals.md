# Modalų kūrimo taisyklės (Livewire / Blade / Alpine)

Šios taisyklės pritaikytos **Livewire 4 + Blade + Alpine** aplinkai.  
Tikslas – stabilūs, nuspėjami ir UX-teisingi modalai be „ghost bugų“.

---

## 1. Modalas yra UI komponentas, ne „page feature“
- Modalas turi būti **atskiras UI komponentas** (`<x-ui.modal>`).
- Visas HTML, ARIA, focus, scroll ir overlay elgesys turi būti **komponente**, ne kiekviename puslapyje.
- Modalas turi aiškų API (props, slots, events).
- Nekeičiame 10–20 failų tam pačiam elgesiui.

---

## 2. Modalas turi vieną „open“ būseną
- Vienas boolean: `open` / `isOpen`.
- Modalas **nevaldomas tiesioginiais DOM hackais**.
- UI yra **būsenos pasekmė**, ne atvirkščiai.

> Leidžiami du render režimai (žr. #4).

---

## 3. Uždarymas privalo veikti 3 būdais
Visada turi veikti:
- `ESC`
- Backdrop click
- Close mygtukas (X)

Visi trys **kviečia tą pačią `close()` logiką**.

---

## 4. Render strategija priklauso nuo turinio
Modalas **gali būti dviejų tipų**:

### 4.1 Unmount (render-if)
Naudoti kai:
- confirm modalai
- paprasti informaciniai modalai
- nėra kliento pusės state

Leidžiama:
```blade
@if ($open)
    <x-ui.modal />
@endif
