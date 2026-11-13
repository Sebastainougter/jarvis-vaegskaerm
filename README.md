# Vægskærm

Statisk side til en altid-tændt iPad (landscape) i J.A.R.V.I.S-tema: cyan HUD på mørk baggrund, roterende arc-reaktor med uret i midten, paneler med hjørnemarkeringer, monospace-skrift. På dansk, store skrifttyper.

Viser:
- Ur, dato og ugenummer
- Dagens familieplan (faste regler pr. ugedag i `index.html`)
- Nedtællinger til fødselsdage, jul og andre begivenheder
- Næste affaldsafhentning fra `data.json`
- Dagens citat
- Beskeder og alarmer fra et Google Sheet (gviz-feed, faneblade `alerts` og `i_dag`), med lyd og oplæsning efter ét tryk
- To kamerafelter (Indkørsel og Firmabil) med live-feed fra UniFi Protect-sharelinks, hentet fra sheet-fanen `indstillinger`

## Opdatering af data
`data.json` kan redigeres uden at røre koden:
- `affald`: liste af `{ "dato": "ÅÅÅÅ-MM-DD", "typer": ["..."] }`. Kun kendte datoer.
- `ekstra_begivenheder`: liste af `{ "navn": "...", "dato": "ÅÅÅÅ-MM-DD", "slut": "ÅÅÅÅ-MM-DD", "ikon": "📅" }` til nedtællingen.

## Alarmer
Sheet-fanen `alerts` har kolonnerne `tidspunkt, kategori, prioritet, tekst, udløber`. Nye rækker fra det seneste døgn vises, giver en lyd og læses op. `prioritet` = `høj` giver rød markering.

## Kamera
Sheet-fanen `indstillinger` har kolonnerne `nøgle` og `værdi`. Siden henter nøglerne `kamera_url` (Indkørsel) og `kamera_url_2` (Firmabil) sammen med de øvrige feeds hvert minut. Indsæt et nyt UniFi-sharelink (`https://monitor.ui.com/...`) i den pågældende rækkes `værdi`-celle, når det gamle udløber. Siden genindlæser kun iframe'en, hvis adressen ændrer sig. En tom eller ugyldig værdi viser "KAMERA OFFLINE · intet link" (eller "ugyldigt link"). Linkene skal ikke skrives ind i koden.

Et sharelink tillader typisk kun én seer ad gangen, og visse kameraer kan bruge en codec (fx H.265 / Enhanced), som iPad Safari ikke afspiller. I de tilfælde viser UniFis egen side en fejl inde i feltet; det kan ikke læses på tværs af iframe-grænsen.

## Opdatering
Beskeder hvert minut. Hver time hentes alle data igen, og siden genindlæses kun, hvis der er udgivet en ny version (så lyden forbliver aktiveret). Kl. 04 laves en daglig opfriskning. Tilføj `?reload=1` for at tvinge en fuld genindlæsning hver time.

Siden indeholder ingen hemmeligheder, kun ID'et på et sheet, som er delt som "alle med linket kan se".
