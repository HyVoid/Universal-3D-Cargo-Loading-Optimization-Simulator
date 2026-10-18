[ 🌐 عربي ](README.ar.md) | [ 🇩🇪 Deutsch ](README.de.md) | [ 🇫🇷 Français ](README.fr.md) | [ 🇳🇱 Nederlands ](README.nl.md) | [ 🇪🇸 Español ](README.sp.md) | [ 🇨🇳 中文 ](README.zh.md) | [ 🇬🇧 English ](README.md)
# 🚛 Universele 3D-simulator voor optimale containerbelading

## ❓ Probleem

Bij verzending wordt „hoeveel dozen passen in één container“ vaak op ervaring geschat — met meestal een van twee uitkomsten: ondervulling en verspilde vrachtkosten, of capaciteitsoverschrijding op het laatste moment en gehaaste containerwissel. Zelfs met een getal weet je vaak niet *hoe* in te laden — welke oriëntatie tegen de wand, waar te beginnen met laden, of of de lading onderweg verschuift en botst.

---

## 🔍 Waarom het gebeurt

3D-bin-packing is fundamenteel een NP-hard probleem. Naarmate de combinatie van doos- en containerafmetingen groeit, groeit het aantal haalbare indelingen exponentieel — uitputtende handmatige berekening is niet praktisch uitvoerbaar. Zelfs bij één enkele productspecificatie kunnen enkele centimeters verschil in de oriëntatie van de doos tegen de inwendige breedte van de container aan de achterkant opstapelen tot een grote dode zone.

Bestaande professionele inpaksoftware is ofwel gericht op logistieke ondernemingen tegen prohibitieve kosten, of komt met een complexe interface die niet praktisch is voor snelle schatting vóór verzending.

---

## 💰 Zakelijke consequentie

- Een daling van het laadpercentage met 5% vertaalt zich direct in 5%–8% hogere effectieve vrachtkosten voor die zending
- Zijdelingse ladingsbeweging en botsingschade tijdens transport komen veel voor in drooggoedvervoer, maar worden vaak afgedaan als „normale slijtage en verlies“ zonder gekwantificeerde tracking
- Zonder een duidelijk laadcijfer bestellen verschepers standaard een extra container „voor de zekerheid“ — een gewoonte die op schaal aanzienlijke kosten accumuleert

---

## 💡 Oplossingslogica

Deze simulator pakt deze kwesties aan via vier kernmechanismen:

**① Nulspeling-antiwiebelalgoritme**

Test uitputtend beide oriëntaties (lengte × breedte) van het product om de indeling te vinden die exact past bij de inwendige breedte van de container, waardoor zijdelingse speling bij de bron wordt geëlimineerd.

**② Diep-eerst-laadlogica**

Laadt van de achterkant van de container naar voren, houdt het zwaartepunt stabiel en maakt lossen aan de deurzijde eenvoudig — consistent met standaard veldpraktijk.

**③ Vierzijdige buffermanagement**

Maximaliseert ruimtebenutting en stuurt de verdeling van openingen tussen lading en alle interieurwanden, waardoor het risico op ladingsinslag door transporttrillingen daalt.

**④ Fysica-gebaseerde zwaartepuntstabilisatie**

Past strikt de volgorde „onder-eerst → achter-eerst“ toe, voorkomt dat lading los drijft en houdt het zwaartepunt van het voertuig naar voren, in overeenstemming met veiligheidsnormen voor wegtransport.

---

## 📋 Werkmap

**Stap 1: Open de simulator**

[Klik hier om de simulator te openen →](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**Stap 2: Voer parameters in** (eenheid: **cm**)

| Parameter | Beschrijving |
|-----------|-------------|
| 🚚 Containerafmetingen | Werkelijk bruikbare inwendige lengte, breedte en hoogte van uw vrachtwagen of container |
| 📦 Productafmetingen | Buitenste dooslengte, -breedte en -hoogte (hoogte staat vast rechtop; het algoritme wisselt alleen lengte en breedte) |
| 🎯 Doel-laad aantal | Voer uw orderhoeveelheid in; laat leeg of stel in op `0` om de maximale containercapaciteit te berekenen |

**Stap 3: Genereer plan**

Klik op de blauwe knop **„Optimaal 3D-plan genereren“**. Het systeem voert de berekening uit en levert automatisch een 3D-visualisatie.

**Stap 4: Interactie & review**

| Actie | Functie |
|--------|----------|
| 🖱️ Linksklikken & slepen | 360° panoramarotatie |
| 🖱️ Rechtsklikken & slepen | Weergave verschuiven |
| ⚙️ Muiswiel | Inzoomen voor detail of uitzoomen voor overzicht |
| 📊 Statistiekdashboard | Verschijnt automatisch na generatie en toont capaciteitslimiet, openingbreedtes en resterende ruimte bij de deur |

---

## 📌 Voorbeeld

**Scenario**: Een verscheper plant de verzending van 800 dozen. Elke doos meet 60×40×30 cm (buitenafmetingen). De beoogde container heeft inwendige afmetingen van 1200×240×260 cm.

**Invoer**: Voer bovenstaande afmetingen in het bedieningspaneel in, stel het doel-laad aantal in op `800` en klik op „Optimaal 3D-plan genereren“.

**Uitvoer**: Het systeem selecteert de oriëntatie die het beste past bij de containerbreedte, rendert de volledige indeling laag voor laag in 3D en levert: werkelijk laadbare hoeveelheid, zijdelingse opening per rij en longitudinale dode ruimte aan de achterkant.

**Beslissingsreferentie**: Als het optimale plan 780 dozen oplevert tegen een doel van 800, kan de verscheper beoordelen of hij de zending splitst, doosafmetingen aanpast of een aanvaardbare tolerantie met de koper bevestigt.

---

## ⚠️ Beperkingen

- Ondersteunt **één enkele productspecificatie** — gemengd multi-SKU laden is nog niet beschikbaar
- Het algoritme werkt op absolute fysieke grenzen. Voor echte operaties wordt aanbevolen om **een tolerantie marge van 25 cm** van de containerafmetingen af te trekken om rekening te houden met doosvervorming, stapelafwijking en arbeidsruimte
- Niet geschikt voor gekoelde houdbare waren, breekbare goederen of lading die gespecialiseerde zekering vereist
- De 3D-render is een planningsillustratie, geen formeel laadinstructiedocument

---

## 🔬 Over de methode

Deze simulator gebruikt een **deterministisch uitputtend algoritme** — geen heuristisch zoeken of AI-generatie. Identieke invoer levert altijd identieke uitvoer; het proces is volledig reproduceerbaar.

Technologiestack: HTML5 / CSS3 / JavaScript (ES6), [Three.js](https://threejs.org/) (WebGL 3D-renderengine), [Tailwind CSS](https://tailwindcss.com/) (geladen via CDN). Het hele tool is verpakt als **één `.html`-bestand** — geen Node.js, Python of database vereist. Dubbelklik en draai in elke moderne browser.

**Deze tool is volledig gratis voor planning van standaard droge lading. Niet geschikt voor gekoelde houdbare waren of breekbare artikelen.**

---

## 📄 Licentie

Dit project is gelicentieerd onder de **MIT License** — vrij te gebruiken, wijzigen en distribueren met naamsvermelding.
