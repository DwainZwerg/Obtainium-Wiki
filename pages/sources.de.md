---
title: App-Quellen
description: Informationen spezifisch für einzelne Quellen
---

# App-Quellen

Die Art und Weise, wie eine App hinzugefügt, auf Aktualisierungen geprüft und installiert wird, hängt von der Quelle und den vom Benutzer für diese App konfigurierten Einstellungen ab.

Die folgenden Optionen sind für alle Anwendungen unabhängig von der Quelle
verfügbar:

- **Nur nachverfolgen**: Wenn Sie diese Option aktivieren, können Sie Aktualisierungsbenachrichtigungen für Apps erhalten, ohne zu versuchen, deren APKs herunterzuladen. Dies ist nützlich, um Updates für Apps zu verfolgen, für die keine APKs verfügbar sind oder die nicht einfach von Obtainium extrahiert werden können. Einige Quellen sind ausschließlich zum nachverfolgen – zum Beispiel [ApkMirror](#apkmirror). Beachten Sie, dass die [Versionserkennung](app_tracking.de.md/#version-detection) nicht für Apps funktioniert, die als „Nur nachverfolgen“ hinzugefügt wurden.
- **APKs nach regulären Ausdrücken filtern**: Wenn mehr als eine APK für eine App-Veröffentlichung verfügbar ist, wird der Benutzer aufgefordert, eine manuell auszuwählen. Dies ist nicht nur unbequem, sondern bedeutet auch, dass die App nicht im Hintergrund aktualisiert wird, auch wenn dies sonst möglich gewesen wäre. Mit dieser Option kann der Benutzer einen regulären Ausdruck angeben, mit dem die APKs herausgefiltert werden können, die nicht erwünscht sind (idealerweise bis hin zu einer Option).
- **Regulären Ausdruck invertieren (APKs nach regulärem Ausdruck filtern)**: Mit dieser Option, kann der reguläre Ausdruck invertiert werden, sodass im regulären Ausdruck die gesuchte APK angegeben werden kann.
- **Nach Möglichkeit versuchen, APKs nach CPU-Architektur zu filtern**: Mit dieser Option wird Obtainium angewiesen, automatisch alle APKs herauszufiltern, die nicht mit dem Gerät des Benutzers kompatibel zu sein scheinen. Die dafür verwendete Logik ist sehr einfach und basiert auf dem APK-Dateinamen. Sie ist daher nicht immer zuverlässig und der Benutzer muss in vielen Fällen immer noch selbst filtern.
- **App-Name**: Hier kann der Benutzer seinen eigenen Namen für die App angeben, anstatt den von Obtainium extrahierten zu nutzen.
- **Von Hintergrundaktualisierungen (falls aktiviert) ausschließen**: Mit dieser Option wird verhindert, dass die Anwendung im Hintergrund aktualisiert wird, selbst wenn Hintergrundaktualisierungen aktiviert sind und die Anwendung ansonsten alle Kriterien für eine Aktualisierung im Hintergrund erfüllt hätte.
- **Update-Benachrichtigungen vermeiden**: Mit dieser Option wird Obtainium angewiesen, den Benutzer nicht zu benachrichtigen, dass für diese App ein Update verfügbar ist oder dass sie im Hintergrund aktualisiert wurde.

Abgesehen davon hat jede Anwendung zusätzliche quellenspezifische Optionen. Die meisten dieser Optionen sind selbsterklärend und werden häufig aktualisiert, so dass sie in diesem Wiki nicht behandelt werden. Einige Quellen haben jedoch einzigartige Verhaltensweisen, die einer genaueren Erläuterung bedürfen und die im Folgenden behandelt werden.

## Currently supported App sources

- Open Source - General:
    - [GitHub](https://github.com/)
    - [GitLab](https://gitlab.com/)
    - [Forgejo](https://forgejo.org/) ([Codeberg](https://codeberg.org/))
    - [F-Droid](https://f-droid.org/)
    - Third Party F-Droid Repos
    - [IzzyOnDroid](https://android.izzysoft.de/)
    - [SourceHut](https://git.sr.ht/)
- Other - General:
    - [APKPure](https://apkpure.net/)
    - [Aptoide](https://aptoide.com/)
    - [Uptodown](https://uptodown.com/)
    - [Huawei AppGallery](https://appgallery.huawei.com/)
    - [Tencent App Store](https://sj.qq.com/)
    - Jenkins Jobs
    - [APKMirror](https://apkmirror.com/) (Track-Only)
    - [RuStore](https://rustore.ru/)
- App-Specific:
    - [Telegram App](https://telegram.org)
    - [Neutron Code](https://neutroncode.com)
- Direct APK Link
- "HTML" (Fallback): Any other URL that returns an HTML page with links to APK files

## GitHub

GitHub legt eine Obergrenze für die Anzahl der API-Anfragen fest, die Sie innerhalb eines bestimmten Zeitraums stellen können. Da Obtainium die GitHub-API nutzt, um Versionsinformationen abzurufen, kann es zu einem "Rate Limit"-Fehler kommen, wenn Sie mehr als ein paar Dutzend GitHub-Apps haben. Sie
können dies umgehen, indem Sie ein [persönliches Zugriffstoken](https://docs.github.com/de/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) von GitHub erhalten und es in den Einstellungen von Obtainium speichern (das Token sollte nur die minimale Leseberechtigung benötigen).

GitHub ermöglicht es Entwicklern auch, mehrere Versionen ihrer Anwendung zu hosten. Dies bedeutet in der Regel ältere Versionen derselben Anwendung, kann aber auch Vorabversionen, Varianten usw. umfassen. - Obtainium bietet daher verschiedene Filter, mit denen Sie durch diese navigieren und genau die Versionen auswählen können, an denen Sie interessiert sind

## XAPK-Support

Einige Quellen (wie APKPure) bieten möglicherweise [XAPK-Dateien] (https://apkpure.com/xapk.html) anstelle von APK-Dateien an. Die XAPK-Unterstützung von Obtainium ist unvollständig und funktioniert möglicherweise nicht zuverlässig.
