## MINE REFLEKTIONER

## Layout

Min største udfordring i projektet var at få opsat layoutet optimalt, så sitets indhold ligger i en kolonne i midten med luft omkring (bleed). Men løsningen skulle også kunne bryde dette layout, da noget enkelt indhold går helt til kant i designet. I min løsning har jeg i mit layout.astro-komponent følgende HTML-struktur:

<body>
<Header>
<main>
<slot>
</main>
<Footer>
</body>

På body opsætter jeg et grid med nedenstående struktur:

grid-template-columns: [full-start] 1fr [content-start] minmax(0, var(--content-width)) [content-end] 1fr [full-end];

Jeg placerer main henover alle kolonnerne (grid-column: full), og nedarver derefter grid'et til main med subgrid. Main er faktisk lidt overflødig her, men vigtig for vores skærmlæser.
Så har jeg valgt at lave et section.astro-komponent, som også nedarver grid'et og placeres henover alle kolonnerne (grid-column: full) – præcis som på main. Jeg placerer alle direkte børn af sektionen i content-kolonnen i mit nedarvede grid med nedenstående kode:

\ > \* {
grid-column: content;
}

Nu placeres mit indhold i section.astro-komponent i content kolonnen, men jeg har også mulighed for at placere det til kant med (grid-column: full) i de tilfælde. Når jeg benytter denne, placeres alt til kant, og da designet oftest er differenceret således, at det kun er den ene side af designet i sektionen som går til kant og den anden side er placeret indenfor content kolonnen, benytter jeg denne matematik funktion til rigtig placering i siderne:
max(1rem, 50% - var(--content-width) / 2);

Dette section.astro-komponent giver mig mulighed for at sætte temaer på hver sektion. Dette har jeg gjort ved at tilføje en Astro-property med tema:

const { theme } = Astro.props;

Og herfra har jeg i komponentet stylet følgende temaer: dark, grey, yellow og white, ved at ændre farver. Det er samme teknik, jeg har brugt til at lave forskellige varianter (const { variant } = Astro.props;) af knapper.

Da jeg havde løst udfordringen og opsat et optimalt layout, gik det egentlig mere eller mindre gnidningsfrit med at kode på sitet.

## Komponenter

Jeg har reflekteret over brugen af komponenter. Jeg har valgt at lave komponenter til alle sektioner, da jeg synes, at det gør det mest overskueligt – men det er nok ikke det smarteste.
Normalt ville jeg kun lave komponenter til sektioner/kort/atomer m.m., som bliver brugt mere end ét sted på sitet.

I min løsning genbruger jeg enkelte komponenter. Jeg genbruger mit CoreValues.astro-komponent, som bruges på index-siden og about-siden. Temaet på komponentet ændres med førnævnte tema-property. Her løb jeg ind i udfordringen, at knappen også skal være en anden variant. Derfor laves en Astro-property i mit CoreValues.astro-komponent (const {btnVariant = "primary"} = Astro.props;), som sættes default til primary. Denne btnVariant kan sættes, ved implementering af CoreValues.astro-komponentet på en side.

Så min løsning til at genbruge komponentet og også ændre varianten af knappen ser således ud:

Index-siden:

 <Section theme="dark">
    <CoreValues btnVariant="tertiary"></CoreValues>
  </Section>

About-siden:

<Section theme="grey" >
    <CoreValues></CoreValues> btnVariant er ikke sat, da den er default primary 
  </Section>

## Organisering af CSS

Helt overordnet placerede jeg følgende i min global.css:

- Farver, spacing og fontstørrelser som variabler. Fonte og spacing er flydende, så de tilpasser sig browser-vinduets størrelse.
- Styling af overskrifter, brødtekst og labels (lille tekst, som benyttes over overskrifterne).

Resten af styling har jeg vurderet er komponent-specifikt – der er klart nogle flere stylinger, der kunne have været optimalt at putte enten i mit section.astro-komponent eller i global.css, for ikke at gentage kode i hver komponent.
