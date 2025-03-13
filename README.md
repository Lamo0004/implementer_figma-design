# Opgaveskabelon til Frontend Design tema på Frontend-valgfaget

Se opgavebeskrivelsen på Fronter.

## Medfølgende API

Der medfølger en simpel API, som du kan bruge til at hente data til din opgave. Det er ikke et krav til opgaven, men det kan gøre det nemmere og hurtigere at få tekst og billeder ind i dit projekt.

Dokumentationen til API'et finder du på: [https://frontend-design-theme.netlify.app/](https://frontend-design-theme.netlify.app/).

Her er et eksempel på, hvordan du kan hente data fra API'et:

```astro
const employeesData = await fetch(
  "https://frontend-design-theme.netlify.app/api/employees"
).then((response) => response.json());

console.log(employeesData);
```

## Mine reflektioner

Reflekter kort men fagligt over din løsning med henblik på udfordringerne og successerne ved opgaven.
Fremhæv specifikke kodestumper, der illustrerer brugen af forskellige teknikker og principper (gerne fra undervisningen).
Forklar, hvordan du har organiseret din CSS; hvornår er det globalt, og hvornår er det komponent-specifikt.
