## Medfølgende API

Dokumentationen til API'et finder du på: [https://frontend-design-theme.netlify.app/](https://frontend-design-theme.netlify.app/).

## MINE REFLEKTIONER

Reflekter kort men fagligt over din løsning med henblik på udfordringerne og successerne ved opgaven.
Fremhæv specifikke kodestumper, der illustrerer brugen af forskellige teknikker og principper (gerne fra undervisningen).
Forklar, hvordan du har organiseret din CSS; hvornår er det globalt, og hvornår er det komponent-specifikt.

## Layout

Min største udfordring i projektet var at få opsat layoutet optimalt, så sitets content lægger i en kolonne i midten med luft omkring (bleed). Men løsningen skulle også kunne bryde dette layout, da noget enkelte content går helt til kant i designet. I min løsning har jeg i mit layout.astro komponent følgende HTML-struktur:

<body>
<Header>
<main>
<slot>
</main>
<Footer>
</body>
På body opsætter jeg et grid med nedenstående struktur:
grid-template-columns: [full-start] 1fr [content-start] minmax(0, 1000px) [content-end] 1fr [full-end];
Jeg placerer main henover alle kolonnerne med grid-column: full, og adopterer/nedarver derefter grid'et til main med subgrid.
Så har

## Komponenter

Jeg har reflekteret over brugen af komponenter. Jeg har valgt at lave komponenter til alle sektioner, da jeg synes det gør det mest overskueligt - men det er nok ikke det smarteste.
Normalt ville jeg kun lave komponenter til sektioner/kort/atomer m.m. som bliver brugt mere end ét sted på sitet.
