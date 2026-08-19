# Galactic Getaways — Netwerkforensiese CTF

Jy het 'n pakkieopname (`traffic.pcap`) ontvang wat geneem is terwyl iemand
die fiktiewe ruimtetoerisme-webwerf **Galactic Getaways** besoek het. Die
webwerf lyk soos 'n gewone reiswebwerf — bestemmings, besprekings, 'n
lidmaatskapgedeelte, aflaai, 'n vertrekbord en 'n nuusbrief.

Die besoeker het drie verborge belonings gedurende die sessie ontvang. Nie een
hiervan is sigbaar in die blaaier nie — hulle bestaan slegs in die
netwerkverkeer. Jou taak is om uit te vind watter HTTP-gesprekke saak maak
en al drie te herstel.

**Belangrik:** geen vlag word as gewone `FLAG{...}` teks gestuur nie. Elkeen
is Base64-geskakel en weggesteek op 'n ander plek: een in die HTML van 'n
bladsy, een in 'n HTTP-antwoordkoptekst, en een in 'n JSON-antwoordliggaam.

## Vaardighede wat jy sal benodig

- **Follow TCP Stream** (regs-klik op 'n pakkie -> Follow -> TCP Stream)
- **Statistics -> Conversations** om die verkeer te kaarteer
- Vertoonfilters soos `http`, `http.request.method == "POST", 
- Base64-ontkoppeling, bv. `printf '%s' 'VALUE' | base64 -d`

## Hoe om te ondersoek

Die opname bevat 'n mengsel van verkeer: normale bladsyladings, klein
agtergrond JSON-versoeke (vlugstatus, aankondigings, weer), 'n groot
vertrekbord, 'n aanmelding, 'n aflaai, en 'n nuusbriefinsrywing. Nie alles
saak maak nie.

1. Filter na `http` en lys die versoeke (`http.request`).
2. Identifiseer die interessante gebruikerhandelinge: die **aanmelding**, die
   **aflaai**, en die **nuusbriefinsrywing**.
3. **Volg die TCP-stroom** van elk en lees die volle versoek en antwoord —
   insluitend koptekste en bladsybron, nie net wat die blaaier sou wys nie.

## Take

### 1. Die lidmaatskapgedeelte

Iemand het by die webwerf aangemeld gedurende die opname.

- Watter gebruikersnaam en wagwoord is ingedien? Hoeveel pogings was nodig?
- Waarom is dit 'n probleem om hierdie oor gewone HTTP te stuur?

**Vlag 1:** na die suksesvolle aanmelding, is die lid 'n 10%
louerhedek kode gegee. Die blaaier het dit nooit gewys nie — dit is weggesteek
binne die HTML wat die bediener teruggestuur het. Vind dit en ontsleutel dit.

- [ ] Vlag 1 verkry: `FLAG{___________________}`

### 2. Die reisdokumente

Die lid het 'n persoonlike dokument van die webwerf afgelaai.

- Watter lêers is afgelaai? Wat doen die bediener as jy dit aanvra sonder om
  eers aan te meld (probeer `/download`, `/download/itinerary.txt`)?

**Vlag 2:** ontsleutel die instapkaart-skandering data.

- [ ] Vlag 2 verkry: `FLAG{___________________}`

### 3. Die nuusbrief

'n Besoeker het vir die nuusbrief ingeteken vanaf die voetskrif van die webwerf.

- Watter e-posadres is gebruik?
- Die bladsy het slegs 'n kort bevestigingsboodskap gewys. Wat het die bediener
  eintlik teruggestuur?

**Vlag 3:** die antwoord bevat 'n welkome koepon. Onttsleutel dit.

- [ ] Vlag 3 verkry: `FLAG{___________________}`

## Indiening

Dien die drie vlaggies in. Vir elk, let op:

- die HTTP-versoek wat betrokke was (metode en pad),
- waar presies die waarde weggesteek was (liggaam / koptekst / HTML),
- hoe jy dit ontsleutel het.

## Bonus — sekuriteitsoudit

Lys sekuriteitsprobleme wat sigbaar is:

1. _________________________________________________
2. _________________________________________________
3. _________________________________________________
4. _________________________________________________
