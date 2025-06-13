---
title: Übersicht User Interface
description: Übersicht User Interface (UI) von Otainium
---

# UI-Übersicht

Die Registerkartenleiste am unteren Rand des Bildschirms ist das Hauptinstrument zur Navigation in Obtainium.

## „Apps“-Registerkarte

Dies ist der Hauptbildschirm; er enthält eine Liste der Apps, die von Obtainium überwacht werden, und liefert die grundlegenden Informationen zu jeder App.

Auf dieser Seite können Sie mit den Schaltflächen am unteren Rand des Bildschirms verschiedene Vorgänge (wie Löschen, Aktualisieren, Markieren usw.) für mehrere Apps auf einmal durchführen. Dies kann nach Auswahl einer oder mehrerer Apps erfolgen, entweder durch langes Drücken, oder über die Schaltfläche „Alle auswählen“, um in den Mehrfachauswahlmodus zu gelangen.

Sie können auch Apps suchen und nach bestimmten Apps filtern, indem Sie auf die Schaltfläche 🔍 klicken. Auf diese Weise können Sie nur die Apps anzeigen, die bestimmte Kriterien erfüllen (z. B. installiert/nicht installiert, aktuell/veraltet, Quellseite usw.).

## „App hinzufügen“-Registerkarte

Auf dieser Seite können Sie eine Anwendung anhand ihrer Quell-URL hinzufügen.

Bei der Eingabe der Quell-URL erkennt Obtainium automatisch, welche [Quellenlogik](app_tracking.de.md/#grundlagen) verwendet werden soll, und zeigt die entsprechenden Optionen an. Wenn eine URL keiner unterstützten Quelle entspricht, wird die „[HTML](sources.de.md/#html)“-Quelle als Standard ausgewählt. Diese Quelle ist ein allgemeiner Fallback, der in einigen Fällen funktionieren kann. Wenn Sie der Meinung sind, dass Obtainium die falsche Wahl getroffen hat, können Sie den zu verwendenden Quellentyp mithilfe des Dropdown-Menüs manuell festlegen.

Bei den meisten Quellen müssen Sie die URL nicht genau angeben. Die GitHub-Quelle akzeptiert beispielsweise jede GitHub-URL, die die Basis-URL des Projektarchivs enthält (z.B. `https://github.com/ImranR98/Obtainium/releases/latest` wird automatisch auf `https://github.com/ImranR98/Obtainium` gekürzt). Ihre URL muss jedoch präziser sein in zwei Situationen:

1. Bei Verwendung der HTML-Quelle
      - Zum Beispiel ist die Tor Android APK unter ´https://www.torproject.org/download/` zu finden, also würde die Eingabe von ´https://www.torproject.org/` nicht funktionieren.
2. Bei der manuellen Auswahl einer Quelle (die die HTML-Fallback-Auswahl von Obtainium außer Kraft setzt)

Auf dieser Seite können Sie auch nach Apps in allen Quellen suchen, die diese Funktion unterstützen (die Registerkarte [Import/Export](ui_overview.de.md/#„Import/Export“-Registerkarte) bietet auch ein separates Suchwerkzeug). Nur weil eine App in den Suchergebnissen auftaucht, heißt das nicht, dass sie erfolgreich hinzugefügt wird – sie muss noch alle anderen Kriterien erfüllen.

Schließlich werden auf dieser Seite alle unterstützten Quellen aufgelistet, zusammen mit zusätzlichen Informationen, z. B. ob eine Quelle durchsuchbar ist.

## „Import/Export“-Registerkarte

Auf dieser Seite können Sie Ihre Obtainium-Daten exportieren, damit sie später importiert werden können. Sie können auch automatische Exporte aktivieren, die immer dann erfolgen, wenn sich Daten ändern.

Auf dieser Seite finden Sie auch verschiedene andere Möglichkeiten, eine große Anzahl von Anwendungen zu importieren, unter anderem über die Suche.

Auch mit dem Suchwerkzeug auf dieser Seite können Sie Quellen durchsuchen, bei denen Sie den Quellhost/die Quelldomäne angeben müssen, z.B. [F-Droid-Repos von Drittanbietern](sources.de.md/#f-droid-third-party-repo).

## „Einstellungen“-Registerkarte

Diese Seite bietet verschiedene Einstellungen für die Benutzeroberfläche und das Verhalten, einschließlich der Möglichkeit, mehr Funktionen für bestimmte Quellen zu aktivieren, indem die erforderlichen Anmeldedaten hinzugefügt werden.
