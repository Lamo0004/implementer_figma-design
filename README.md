## Medfølgende API

API: [https://frontend-design-theme.netlify.app/](https://frontend-design-theme.netlify.app/).

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
Jeg placerer main henover alle kolonnerne (grid-column: full), og nedarver derefter grid'et til main med subgrid. Main er faktisk lidt overflødig, men vigtig for vores skærmlæser.
Så har jeg valgt at lave et section.astro komponent, som også nedarver grid'et og placeres henover alle kolonnerne (præcis det samme som main).
Jeg placerer alle direkte børn af sektionen i content kolonnen i nedarvede mit grid, som jeg har nedarvet et par gange efterhånden. > \* {
grid-column: content;
}
Dette section.astro komponent giver mig mulighed for at sætte temaer på hver sektion. Dette har jeg gjort ved at tilføje en astro property med tema:
const { theme } = Astro.props;
Og herfra har jeg i komponetet stylet følgende temaer: dark, grey, yellow og white, ved at ændre farver.

Det er samme teknik jeg har brugt til at lave forskellige varianter (const { variant } = Astro.props;) af knapper.

Da jeg havde løst den største udfordringen og opsat et optimalt layout, gik det egentlig mere eller mindre gnidningsfri med at kode sitet.

## Komponenter

Jeg har reflekteret over brugen af komponenter. Jeg har valgt at lave komponenter til alle sektioner, da jeg synes det gør det mest overskueligt - men det er nok ikke det smarteste.
Normalt ville jeg kun lave komponenter til sektioner/kort/atomer m.m. som bliver brugt mere end ét sted på sitet.

I min løsning genbruger jeg enkelte komponeter. Jeg genbruger selvfølgelig min header og footer.  
Jeg genbruger også mit CoreValues.astro komponent, som bruges på index-siden og about-siden. Temaet på komponentet ændres med førnævnte tema property. Her løb jeg ind i udfordringen, at knappen også skulle være en anden variant. Derfor lavede jeg en astro property i mit CoreValues.astro komponent (const {btnVariant = "primary"} = Astro.props;), som jeg satte default til primary. Denne btnVariant kunne jeg så sætte når jeg indsætte CoreValues.astro komponentet på en side.

Så min løsning til at genbruge komponentet og også ændre varianten af knappen ser således ud:

Index-siden:

 <Section theme="dark">
    <CoreValues btnVariant="tertiary"></CoreValues>
  </Section>

About-siden:

<Section theme="grey" >
    <CoreValues></CoreValues> btnVariant er ikke sat, da den er default primary 
  </Section>

## CSS

Forklar, hvordan du har organiseret din CSS; hvornår er det globalt, og hvornår er det komponent-specifikt.
Organisering af CSS har jeg mistet overblikket lidt over. Men helt overordnet placerede jeg følgende i min global.css:

- farver, spacing og font størrelser som variabler. Fonte og spacing er flydende, så de tilpasser sig browser-vinduets størrelse.
- styling af overskrifter, brødtekst og label (lille tekst, som benyttes over overskrifterne)

Resten af styling har jeg vurderet er komponent-specifikt – der er klar nogle flere stylinger der kunne have været optimalt at putte enten i mit section.astro komponent eller i global.css, for ikke at gentage kode i hver komponent.
