---
layout: page
title: Datenschutzerklärung der App „Soll ich lüften?“
permalink: /soll-ich-lueften/datenschutz.html
---

Diese Datenschutzerklärung gilt für die iPhone-App „Soll ich lüften?“. Sie beschreibt, welche personenbezogenen Daten die App verarbeitet, wohin sie gehen und welche Rechte du hast.

## Kurzfassung

- Deine Messwerte, der Verlauf und deine Einstellungen bleiben auf deinem iPhone.
- Ein Foto eines Thermometers verlässt das iPhone nur, wenn du vorher zugestimmt hast. Es geht über einen Server bei Cloudflare an den KI-Dienst Claude von Anthropic und wird dort nur zum Auslesen der Werte verwendet.
- Deinen Standort nutzt die App nur, wenn du „Wetter am Standort verwenden“ wählst. Er geht dann an Apples Wetterdienst.
- Es gibt kein Konto, keine Werbung, kein Tracking und keine Nutzungsanalyse.

## Verantwortlicher

Michael Kühnel  
Berlepschstraße 4  
34119 Kassel  
Deutschland  
E-Mail: <mail@michael-kuehnel.de>

Siehe auch [Impressum](/impressum.html).

## Daten, die auf deinem iPhone bleiben

Eingegebene und erkannte Temperaturen und Luftfeuchten, der Verlauf gespeicherter Ergebnisse und deine Einstellungen (z. B. ob die App das Wetter am Standort laden darf) speichert die App nur lokal auf deinem iPhone. Sie werden nicht an mich oder Dritte übertragen. Wenn du die App löschst, sind diese Daten ebenfalls gelöscht.

Fotos, die du in der App aufnimmst, speichert die App weder in deiner Mediathek noch anderswo auf dem Gerät. Fotos aus der Mediathek wählst du über die Auswahl von iOS aus; die App erhält dabei nur das gewählte Foto und keinen Zugriff auf deine übrigen Fotos.

## Auslesen von Thermometer-Fotos

**Was passiert:** Wenn du ein Thermometer, Hygrometer oder eine Wetterstation fotografierst, verkleinert die App das Foto und sendet es an einen von mir betriebenen Server (Proxy) bei Cloudflare. Der Proxy leitet das Foto an die Claude-API von Anthropic weiter. Claude erkennt Temperatur und Luftfeuchte auf dem Foto, die Werte gehen als Text an die App zurück.

**Welche Daten:** das Foto. Je nach Motiv kann es außer dem Thermometer weitere Inhalte zeigen, z. B. Teile deiner Wohnung. Fotografiere deshalb möglichst nur das Display. Name, Konto oder Standort werden dabei nicht mitgesendet.

**Rechtsgrundlage:** deine Einwilligung (Art. 6 Abs. 1 lit. a DSGVO). Die App fragt vor dem ersten Foto danach. Du kannst die Einwilligung jederzeit in der App unter Einstellungen → „Fotos an Claude senden“ widerrufen; danach lassen sich die Werte nur noch eintippen. Der Widerruf gilt für die Zukunft.

**Speicherdauer:** Der Proxy speichert das Foto nicht, er reicht es nur durch. Anthropic löscht Eingaben und Ausgaben der API nach eigenen Angaben automatisch innerhalb von 30 Tagen, außer bei Verstößen gegen die Nutzungsrichtlinien oder gesetzlichen Pflichten. Daten aus der API verwendet Anthropic nicht zum Training seiner Modelle.

## Schutz vor Missbrauch (App Attest und Tageslimit)

Damit nur die echte App den Proxy nutzen kann, verwendet sie Apples App Attest. Dabei erzeugt das iPhone einen kryptografischen Schlüssel, Apple bestätigt dessen Echtheit, und die App signiert damit jede Anfrage. Der Proxy speichert dafür:

- eine zufällige Kennung dieses Schlüssels und den zugehörigen öffentlichen Schlüssel,
- einen Zähler der Anfragen (gegen das Wiederverwenden abgefangener Anfragen),
- die Zahl der Fotos am aktuellen Tag (Tageslimit).

Diese Daten lassen keinen Rückschluss auf deinen Namen, deine Apple-ID oder dein Gerät zu. Sie werden 90 Tage nach der letzten Nutzung automatisch gelöscht.

**Rechtsgrundlage:** mein berechtigtes Interesse, den Dienst vor Missbrauch und unbegrenzten Kosten zu schützen (Art. 6 Abs. 1 lit. f DSGVO).

## Server-Protokolle

Beim Aufruf des Proxys verarbeitet Cloudflare technisch notwendige Verbindungsdaten, insbesondere deine IP-Adresse, Datum und Uhrzeit sowie die aufgerufene Adresse. Die IP-Adresse dient außerdem einer Begrenzung der Anfragen pro Minute. Protokolle der Anfragen werden zur Fehleranalyse höchstens 7 Tage aufbewahrt. Fotos sind darin nicht enthalten.

**Rechtsgrundlage:** mein berechtigtes Interesse am sicheren und stabilen Betrieb (Art. 6 Abs. 1 lit. f DSGVO).

## Wetter am Standort

Nur wenn du „Wetter am Standort verwenden“ wählst und iOS den Standortzugriff erlaubst, ermittelt die App deinen Standort und fragt bei Apples Wetterdienst (WeatherKit) Temperatur und Luftfeuchte für diesen Ort ab. Der Standort geht dabei direkt an Apple, nicht an mich, und die App speichert ihn nicht. Apple verwendet den Standort nach eigenen Angaben nur, um die Wetterdaten zu liefern, und verknüpft ihn nicht mit deiner Apple-ID.

**Rechtsgrundlage:** deine Einwilligung (Art. 6 Abs. 1 lit. a DSGVO). Du kannst den Standortzugriff jederzeit in den iOS-Einstellungen unter Datenschutz & Sicherheit → Ortungsdienste widerrufen.

## Empfänger und Übermittlung in die USA

- **Cloudflare, Inc.**, 101 Townsend St., San Francisco, CA 94107, USA: Betrieb des Proxys als Auftragsverarbeiter (Art. 28 DSGVO). [Datenschutzerklärung von Cloudflare](https://www.cloudflare.com/privacypolicy/)
- **Anthropic, PBC**, 548 Market St, PMB 90375, San Francisco, CA 94104, USA: Auslesen der Fotos als Auftragsverarbeiter. [Datenschutzerklärung von Anthropic](https://www.anthropic.com/legal/privacy)
- **Apple Inc.**, One Apple Park Way, Cupertino, CA 95014, USA: App Attest und WeatherKit. [Datenschutzerklärung von Apple](https://www.apple.com/de/legal/privacy/)

Dabei werden Daten in die USA übermittelt. Grundlage sind der Angemessenheitsbeschluss der EU-Kommission zum EU-US Data Privacy Framework, soweit der Empfänger danach zertifiziert ist, und andernfalls die Standardvertragsklauseln der EU-Kommission (Art. 46 Abs. 2 lit. c DSGVO), die Bestandteil der Vereinbarungen zur Auftragsverarbeitung sind.

Für Download und Updates der App gilt die Datenschutzerklärung von Apple. Auf diese Verarbeitung habe ich keinen Einfluss.

## Deine Rechte

Du hast das Recht auf Auskunft (Art. 15 DSGVO), Berichtigung (Art. 16), Löschung (Art. 17), Einschränkung der Verarbeitung (Art. 18), Datenübertragbarkeit (Art. 20) und Widerspruch gegen Verarbeitungen auf Grundlage berechtigter Interessen (Art. 21). Erteilte Einwilligungen kannst du jederzeit mit Wirkung für die Zukunft widerrufen (Art. 7 Abs. 3). Schreib mir dazu eine E-Mail an <mail@michael-kuehnel.de>.

Da ich keine Daten speichere, die dich identifizieren, kann ich dir Daten des Proxys in der Regel keiner Person zuordnen (Art. 11 DSGVO). Die Daten auf deinem iPhone kannst du selbst löschen, indem du Einträge im Verlauf entfernst oder die App löschst.

Außerdem hast du das Recht, dich bei einer Datenschutz-Aufsichtsbehörde zu beschweren (Art. 77 DSGVO). Für mich zuständig ist:

Der Hessische Beauftragte für Datenschutz und Informationsfreiheit  
Gustav-Stresemann-Ring 1  
65189 Wiesbaden  
<https://datenschutz.hessen.de>

## Änderungen

Ich passe diese Datenschutzerklärung an, wenn sich die App oder die rechtlichen Anforderungen ändern. Es gilt die jeweils hier veröffentlichte Fassung.

Stand: Oktober 2026
