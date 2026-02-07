# dev-notes
# Dev Notes

Asmeninės programavimo pastabos, taisyklės ir patternai.

Šis repo skirtas:
- fiksuoti sprendimus ir pamokas
- nekartoti tų pačių klaidų kuriant naujus projektus
- turėti vieną vietą architektūriniams ir UI sprendimams

Tai **ne tutorialai ir ne dokumentacija kitiems** – tai praktinės taisyklės sau.

---

## Struktūra

- `ui/`  
  Bendros UI elgsenos taisyklės (modalai, formos, lentelės ir pan.)

- `architecture/`  
  Bendri architektūriniai patternai ir sprendimai

- `stacks/`  
  Konkrečių technologijų pastabos:
  - `laravel/`
  - `javascript/`
  - `python/`
  - ir kt.

---

## Kaip naudoti

- Jei šiandien pataisei bug’ą → rytoj užrašyk taisyklę
- Jei kažkas „atrodo blogai“ → suformuluok kodėl
- Rašyti trumpai, be teorijos
- Jei taisyklė galioja visur → dėti į `ui/` arba `architecture/`
- Jei tik konkrečiam stack’ui → dėti į `stacks/<tech>/`

---

## Principai

- Paprastumas > „protingumas“
- Aiškios taisyklės > spėjimai
- Viena tiesa vienoje vietoje
- Jei kažką reikia prisiminti – vadinasi reikia užrašyti
