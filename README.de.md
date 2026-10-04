# Trayme

[English](README.md) | **Deutsch**

Eine kleine portable Windows-App, die Fenster beim Minimieren in den Infobereich (Tray) verschiebt.
Mit Regeln (RegEx auf Fenstertitel und/oder Prozessname) können Fenster auch beim **Schließen** in den Infobereich wandern.

![Einstellungsfenster](docs/screenshot.png)

- Eine einzige `Trayme.exe` (~180 KB), keine Installation; nutzt das .NET Framework 4.8, das bei Windows 10/11 dabei ist
- Einstellungen in `Trayme.xml` neben der EXE
- Die einzigen Änderungen außerhalb des eigenen Ordners, beide optional: der Autostart-Eintrag unter `HKCU\…\Run` und eine Verknüpfung im Startmenü des Benutzers
- Oberfläche auf Deutsch und Englisch (richtet sich nach der Windows-Sprache, umschaltbar in den Einstellungen)
- Windows-11-Look: folgt dem Hell-/Dunkelmodus und der Akzentfarbe

## Download

- **[Neueste Version](https://github.com/naderi/trayme/releases/latest)** – `Trayme.exe` herunterladen, in einen beliebigen Ordner legen und starten.
- Oder mit [Scoop](https://scoop.sh):

  ```
  scoop bucket add naderi https://github.com/naderi/scoop-bucket
  scoop install naderi/trayme
  ```

## Bedienung

- **Klick auf das Trayme-Symbol** öffnet das Menü: versteckte Fenster, der Schalter „Alle Fenster beim Minimieren in den Infobereich“, Einstellungen, Info, Beenden
- **Doppelklick auf das Trayme-Symbol** öffnet die Einstellungen
- **Klick auf das Symbol eines versteckten Fensters** holt es zurück; Rechtsklick → „Programm schließen“ beendet es wirklich
- **Rechtsklick auf den Minimieren-Button** eines beliebigen Fensters schickt es in den Infobereich, unabhängig von den Regeln (in den Einstellungen abschaltbar)
- **Umschalttaste beim Minimieren gedrückt halten**, damit ein Fenster dieses eine Mal in der Taskleiste bleibt
- **Beim Beenden** von Trayme werden alle versteckten Fenster wiederhergestellt
- Ein zweiter Start von `Trayme.exe` öffnet die Einstellungen der laufenden Instanz
- **Info** (im Menü oder über den ⓘ-Button unten links in den Einstellungen) zeigt Version, Entwickler, den GitHub-Link und Programm-Updates

## Regeln

Die erste passende Regel gilt; passt keine, gilt „Alle Fenster beim Minimieren in den Infobereich“.

| Feld | Bedeutung |
|---|---|
| Fenstertitel (RegEx) | .NET-RegEx, ohne Beachtung der Groß-/Kleinschreibung, z. B. ` - Mozilla Thunderbird$` |
| Prozess (RegEx) | Name der EXE, z. B. `^thunderbird\.exe$` |
| Beim Minimieren in den Infobereich | das Fenster wird beim Minimieren versteckt |
| Beim Schließen in den Infobereich | X-Button und Alt+F4 verstecken das Fenster, statt es zu schließen |

Ein leeres Feld passt auf alles; eine Regel ganz ohne Muster wird ignoriert.
Beide Schalter aus = Ausnahme (das Fenster kommt nie in den Infobereich).
„Aus Fenster“ erstellt eine Regel aus einem gerade geöffneten Fenster.

## Grenzen

- „Beim Schließen in den Infobereich“ fängt den X-Button (über einen Maus-Hook und `WM_NCHITTEST`) und Alt+F4 ab.
  **Nicht** abgefangen werden „Schließen“ im Systemmenü, „Fenster schließen“ in der Taskleiste und das Beenden über das programmeigene Menü –
  dafür müsste eine DLL in fremde Prozesse injiziert werden.
- Fenster von Programmen, die als Administrator laufen, lassen sich nur verstecken, wenn Trayme selbst als Administrator läuft.
- Apps mit eigener Titelleiste funktionieren, solange sie über `WM_NCHITTEST` mindestens einen Titelleisten-Button melden (die meisten modernen Apps tun das);
  die Position der Buttons kommt dann von DWM. Apps, die keinen melden (z. B. Audacity 4), werden für Rechtsklick-Minimieren und den X-Button nicht erkannt.

## Programm-Updates

Trayme aktualisiert sich selbst über die [Releases dieses Repositorys](https://github.com/naderi/trayme/releases):

- Einmal am Tag sucht es im Hintergrund nach einer neuen Version (abschaltbar im Info-Fenster: *Automatisch suchen (einmal täglich)*). Eine neue Version wird einmal per Benachrichtigung gemeldet, und der ⓘ-Button in den Einstellungen bekommt einen orangen Punkt.
- Im Info-Fenster: *Nach Updates suchen* → *Update herunterladen* → *Neu starten & aktualisieren*.
- Ein Download wird nur verwendet, wenn seine Signatur (`.sig`) zum in Trayme eingebauten Schlüssel passt; alles andere wird abgelehnt. Versteckte Fenster werden vor dem Neustart wiederhergestellt, `Trayme.xml` bleibt unverändert.
- Mit Scoop installiert, verweist Trayme nur auf `scoop update trayme`.

## Lizenz

Freeware – kostenlos nutzbar, aber **Verkauf verboten**. Siehe [LICENSE](LICENSE).

© 2026 [Ali Naderi](https://github.com/naderi)

## Unterstützung

Wenn Trayme deine Taskleiste aufgeräumt hält, kannst du die Weiterentwicklung auf Ko‑fi unterstützen. ☕

<a href='https://ko-fi.com/N7N123QIX0' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://storage.ko-fi.com/cdn/kofi2.png?v=6' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
