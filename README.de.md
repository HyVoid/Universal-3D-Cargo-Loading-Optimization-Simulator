[ 🌐 عربي ](README.ar.md) | [ 🇩🇪 Deutsch ](README.de.md) | [ 🇫🇷 Français ](README.fr.md) | [ 🇳🇱 Nederlands ](README.nl.md) | [ 🇪🇸 Español ](README.sp.md) | [ 🇨🇳 中文 ](README.zh.md) | [ 🇬🇧 English ](README.md)
# 🚛 Universeller 3D-Simulator zur Optimierung der Containerbeladung

## ❓ Problem

Beim Versand wird „wie viele Kartons passen in einen Container“ oft aus Erfahrung geschätzt — mit meist einem von zwei Ergebnissen: Unterbefüllung und verschwendete Frachtkosten, oder in letzter Minute Kapazitätsüberschreitung und hektischer Containerwechsel. Selbst mit einer Zahl weiß man oft nicht *wie* packen — welche Ausrichtung an die Wand, wo das Beladen beginnen, oder ob die Ladung unterwegs verrutscht und kollidiert.

---

## 🔍 Warum es passiert

3D-Bin-Packing ist grundsätzlich ein NP-schweres Problem. Mit wachsender Kombination aus Karton- und Containerabmessungen wächst die Zahl machbarer Anordnungen exponentiell — erschöpfende manuelle Berechnung ist nicht praktikabel. Schon bei einer einzigen Produktspezifikation können wenige Zentimeter Unterschied in der Ausrichtung des Kartons gegen die Innenbreite des Containers am Heck zu einer großen Totzone aufsummieren.

Bestehende professionelle Packsoftware richtet sich entweder an Logistikunternehmen zu prohibitiv Kosten, oder bringt eine komplexe Bedienoberfläche mit, die für schnelle Abschätzung vor dem Versand ungeeignet ist.

---

## 💰 Geschäftliche Auswirkung

- Ein Rückgang der Beladungsrate um 5 % bedeutet direkt 5 %–8 % höhere effektive Frachtkosten für diese Sendung
- Seitliche Ladungsbewegung und Kollisionsschäden im Transit sind im Trockenfrachtversand häufig, werden aber oft als „normaler Verschleiß und Verlust“ ohne quantifizierte Nachverfolgung abgebucht
- Ohne klare Beladungszahl neigen Versender dazu, vorsichtshalber einen zusätzlichen Container zu bestellen — eine Gewohnheit, die bei großen Volumina erhebliche Kosten akkumuliert

---

## 💡 Lösungslogik

Dieser Simulator adressiert diese Punkte durch vier Kernmechanismen:

**① Nullspalt-Anti-Schwing-Algorithmus**

Testet erschöpfend beide Ausrichtungen (Länge × Breite) des Produkts, um die Anordnung zu finden, die exakt zur Innenbreite des Containers passt, und eliminiert seitliches Spiel an der Wurzel.

**② Tief-zuerst-Beladungslogik**

Lädt vom Heck des Containers nach vorne, hält den Schwerpunkt stabil und macht das Entladen von der Türseite einfach — konsistent mit der üblichen Feldpraxis.

**③ Vier-Seiten-Pufferverwaltung**

Maximiert die Raumnutzung und steuert die Spaltverteilung zwischen Ladung und allen Innenwänden, wodurch das Risiko von Ladungsaufprall durch Transitvibrationen sinkt.

**④ Physikbasierte Schwerpunkt-Stabilisierung**

Wendet strikt die Sequenz „unten-zuerst → hinten-zuerst“ an, verhindert freiliegende Ladung und hält den Fahrzeugschwerpunkt vorn, in Übereinstimmung mit Sicherheitsstandards für den Straßentransport.

---

## 📋 Arbeitsmappe

**Schritt 1: Simulator öffnen**

[Hier klicken, um den Simulator zu öffnen →](https://hyvoid.github.io/Universal-3D-Cargo-Loading-Optimization-Simulator/)

**Schritt 2: Parameter eingeben** (Einheit: **cm**)

| Parameter | Beschreibung |
|-----------|-------------|
| 🚚 Containerabmessungen | Tatsächlich nutzbare Innenlänge, -breite und -höhe Ihres Lkw oder Containers |
| 📦 Produktabmessungen | Äußere Kartonlänge, -breite und -höhe (Höhe steht fest aufrecht; der Algorithmus tauscht nur Länge und Breite) |
| 🎯 Ziel-Beladungszahl | Geben Sie Ihre Auftragsmenge ein; leer lassen oder auf `0` setzen, um die maximale Containerkapazität zu berechnen |

**Schritt 3: Plan generieren**

Klicken Sie die blaue Schaltfläche **„Optimale 3D-Lösung generieren“**. Das System führt die Berechnung aus und gibt automatisch eine 3D-Visualisierung aus.

**Schritt 4: Interagieren & überprüfen**

| Aktion | Funktion |
|--------|----------|
| 🖱️ Linksklick & Ziehen | 360°-Panoramarotation |
| 🖱️ Rechtsklick & Ziehen | Ansicht schwenken |
| ⚙️ Mausrad | Zoomen für Details oder Überblick |
| 📊 Statistik-Dashboard | Erscheint automatisch nach der Generierung und zeigt Kapazitätsgrenze, Spaltbreiten und verbleibenden Raum nahe der Tür |

---

## 📌 Beispiel

**Szenario**: Ein Versender plant den Versand von 800 Kartons. Jeder Karton misst 60×40×30 cm (Außenmaße). Der vorgesehene Container hat Innenmaße von 1200×240×260 cm.

**Eingabe**: Geben Sie die obigen Maße in das Bedienfeld ein, setzen Sie die Ziel-Beladungszahl auf `800` und klicken Sie „Optimale 3D-Lösung generieren“.

**Ausgabe**: Das System wählt die Ausrichtung, die am besten zur Containerbreite passt, rendert die vollständige Anordnung Schicht für Schicht in 3D und gibt aus: tatsächlich beladbare Menge, Seitenspalt pro Reihe und longitudinalen Totraum am Heck.

**Entscheidungsreferenz**: Wenn der optimale Plan 780 Kartons gegen ein Ziel von 800 ergibt, kann der Versender beurteilen, ob er die Sendung aufteilt, Kartonmaße anpasst oder eine akzeptable Toleranz mit dem Käufer bestätigt.

---

## ⚠️ Einschränkungen

- Unterstützt **nur eine Produktspezifikation** — gemischte Multi-SKU-Beladung ist noch nicht verfügbar
- Der Algorithmus arbeitet auf absoluten physischen Grenzen. Für reale Abläufe wird empfohlen, **eine 25-cm-Toleranzmarge** von den Containerabmessungen abzuziehen, um Kartonverformung, Stapelabweichung und Arbeitsfreiraum zu berücksichtigen
- Nicht geeignet für gekühlte verderbliche Ware, zerbrechliche Güter oder Ladung mit spezieller Sicherung
- Das 3D-Rendering ist eine Planungsillustration, kein formelles Beladeanweisungsdokument

---

## 🔬 Über die Methode

Dieser Simulator verwendet einen **deterministischen erschöpfenden Algorithmus** — keine heuristische Suche oder KI-Generierung. Identische Eingaben erzeugen stets identische Ausgaben; der Prozess ist vollständig reproduzierbar.

Technologie-Stack: HTML5 / CSS3 / JavaScript (ES6), [Three.js](https://threejs.org/) (WebGL-3D-Rendering-Engine), [Tailwind CSS](https://tailwindcss.com/) (per CDN geladen). Das gesamte Tool ist als **einzelne `.html`-Datei** verpackt — kein Node.js, Python oder Datenbank erforderlich. Doppelklicken und in jedem modernen Browser ausführen.

**Dieses Tool ist völlig kostenlos für die Planung von Standard-Trockenfracht. Nicht geeignet für gekühlte verderbliche Ware oder zerbrechliche Artikel.**

---

## 📄 Lizenz

Dieses Projekt ist unter der **MIT License** lizenziert — frei zu verwenden, zu modifizieren und mit Namensnennung zu verteilen.
