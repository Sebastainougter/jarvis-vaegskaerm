# Vægskærm

Statisk side til en altid-tændt iPad (landscape). Mørkt tema, store skrifttyper, på dansk.

Viser:
- Ur, dato og ugenummer
- Vejr for Køge fra Open-Meteo (nu, i dag, næste timer, 5 dage, sol op/ned)
- Dagens familieplan (faste regler pr. ugedag i `index.html`)
- Nedtællinger til fødselsdage, jul og andre begivenheder
- Næste affaldsafhentning fra `data.json`
- Dagens citat
- Beskeder og alarmer fra et Google Sheet (gviz-feed, faneblade `alerts` og `i_dag`), med lyd og oplæsning efter ét tryk

## Opdatering af data
`data.json` kan redigeres uden at røre koden:
- `affald`: liste af `{ "dato": "ÅÅÅÅ-MM-DD", "typer": ["..."] }`. Kun kendte datoer.
- `ekstra_begivenheder`: liste af `{ "navn": "...", "dato": "ÅÅÅÅ-MM-DD", "slut": "ÅÅÅÅ-MM-DD", "ikon": "📅" }` til nedtællingen.

## Alarmer
Sheet-fanen `alerts` har kolonnerne `tidspunkt, kategori, prioritet, tekst, udløber`. Nye rækker fra det seneste døgn vises, giver en lyd og læses op. `prioritet` = `høj` giver rød markering.

## Opdatering
Vejr hvert 15. minut, beskeder hvert minut. Hver time hentes alle data igen, og siden genindlæses kun, hvis der er udgivet en ny version (så lyden forbliver aktiveret). Kl. 04 laves en daglig opfriskning. Tilføj `?reload=1` for at tvinge en fuld genindlæsning hver time.

Siden indeholder ingen hemmeligheder, kun ID'et på et sheet, som er delt som "alle med linket kan se".
