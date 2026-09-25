<div align="center">

<img src="assets/logo.png" width="96" height="96" alt="Ereshkigal">

# Ereshkigal Project

**Ein-Klick-Flashen der Ereshkigal-Firmware für WLAN-Sicherheitstests RTL8720DN (BW16).**

Keine Arduino IDE. Kein Quellcode. Keine Kommandozeile. Nur dieser Ordner.

[English](README.md) · [Bahasa Indonesia](README.id.md) · [Español](README.es.md) · [Français](README.fr.md) · **Deutsch** · [中文](README.zh.md)

![version](https://img.shields.io/badge/Version-2.0.0-6c4cf1)
![plattform](https://img.shields.io/badge/Plattform-Windows%2010%2F11-2fa565)
![board](https://img.shields.io/badge/Board-RTL8720DN%20(BW16)-14161d)
![sprachen](https://img.shields.io/badge/UI--Sprachen-6-e0870b)

</div>

> [!WARNING]
> **Rechtlicher & Sicherheitshinweis vor Gebrauch lesen.**
> Ereshkigal ist ein Werkzeug für **WLAN-Sicherheitstests**. Nutze es **nur**:
> - in Netzwerken und an Geräten, die **dir gehören**, oder für die du eine **ausdrückliche schriftliche Erlaubnis** zum Testen hast;
> - in einer **kontrollierten Labor-/Testumgebung**, die du dafür eingerichtet hast.
>
> Setze es **nicht** gegen Netzwerke, Geräte oder Personen ein, für die du keine
> Testerlaubnis hast. Das unbefugte Abhören oder Stören von Funknetzen ist **in den
> meisten Ländern illegal** und kann zu **Strafverfahren** führen. Dieses Projekt
> dient nur der Bildung, Forschung, CTFs und autorisierten Penetrationstests. **Du
> allein bist für die Nutzung verantwortlich.**

---

<p align="center">
  <img src="assets/screenshot-flasher.png" width="330" alt="Ereshkigal Project (Windows)">
  &nbsp;&nbsp;
  <img src="assets/screenshot-device.png" width="300" alt="Web-Oberfläche des Ereshkigal-Geräts">
</p>
<p align="center"><sub>Links: der Flasher unter Windows. Rechts: das integrierte Web-Dashboard des Geräts nach dem Flashen.</sub></p>

## Inhalt

| Datei | Was es ist |
|-------|------------|
| **`EreshkigalFlasher.exe`** | Die Flash-App (Windows, eigenständig). |
| **`Ereshkigal.efw`** | Die Firmware im geschützten Ereshkigal-Format. |

Verteile beide Dateien zusammen. Die App ist ein kleines natives Fenster in
**English, Bahasa Indonesia, Español, Français, Deutsch und 中文** umschaltbar
über die Auswahl oben rechts.

## Voraussetzungen

- **Windows 10 oder 11.** Nutzt die integrierte **WebView2-Runtime** (in Windows 11
  und aktuellem Windows 10 enthalten; andernfalls einmalig die kostenlose
  *Microsoft Edge WebView2 Runtime* installieren).
- Ein **RTL8720DN / BW16**-Board und ein **Daten**-USB-Kabel.
- Der **USB-Seriell-Treiber** des Boards (meist CH340 oder CP2102), damit es als
  `COM`-Port erscheint.

## Anleitung in 4 Schritten flashen

1. **Board anstecken** (USB) und **`EreshkigalFlasher.exe`** starten.
2. `Ereshkigal.efw` ist bereits gewählt. Wähle den **COM-Port** deines Boards aus
   der Liste (Aktualisieren drücken, falls er fehlt Board ab-/anstecken und
   erneut aktualisieren; der neue Eintrag ist dein Board).
3. Lass **Geschwindigkeit** auf `1500000`.
4. **Firmware flashen** klicken, auf **Fertig** warten, dann das Board aus- und
   einschalten.

Die meisten Boards gehen selbst in den Flash-Modus. **Wenn das Protokoll hängt**,
führe die **Download-Modus**-Tastenfolge am Board aus:

```
   ┌── 1 ──┐      ┌── 2 ──┐      ┌── 3 ──┐
   │ BOOT  │  →   │ RESET │  →   │ BOOT  │
   │halten │      │tippen │      │lösen  │
   └───────┘      └───────┘      └───────┘
   BOOT halten · RESET tippen · BOOT loslassen
```

Der Flasher wiederholt die Synchronisierung automatisch (bis zu 3×).

## Erster Start nach dem Flashen

1. Das Gerät sendet ein **offenes** WLAN namens **`Ereshkigal`**.
2. Verbinde dich und öffne **http://192.168.1.1/**.
3. Durchlaufe einmalig den **Einrichtungsassistenten** lege einen Netzwerknamen
   und ein Passwort (8–63 Zeichen) fest. Das Gerät speichert es und startet neu.
4. Verbinde dich mit deinem Passwort neu, öffne **http://192.168.1.1/** erneut, und
   das volle Dashboard ist freigeschaltet.

## Für einen WPA2 → WPA3-Check nutzen

Ereshkigal zeigt eine reale, verbreitete WLAN-Schwäche: Netze mit **WPA2 ohne
Protected Management Frames (PMF / 802.11w)** lassen sich mit gefälschten
**Deauthentication**-Frames stören  jeder in der Nähe kann Clients hinauswerfen,
und diese erzwungene Trennung ist der erste Schritt hinter Handshake-Capture und
Evil-Twin-Angriffen.

Ein typischer **autorisierter** Test im eigenen Netz:

1. **Scan**  Dashboard öffnen, *Scan* antippen, Zielnetz wählen.
2. **Users**  die verbundenen Geräte auflisten.
3. **Attack**  einen *Deauth*-Test starten und die eigenen Clients beobachten.
4. **Detector**  das Funkmodul aufs Erkennen von Deauth-Frames ansetzen.

**Ergebnis deuten**
- Clients **fliegen raus** → das Netz ist WPA/WPA2 ohne erzwungenes PMF und
  anfällig für Management-Frame-Spoofing (Deauth-DoS und die anschließende
  Trennen-dann-Mitschneiden-Kette).
- Clients **bleiben verbunden** → die Management-Frames sind geschützt.

**Die Lösung  auf WPA3 wechseln.** Stelle das Netz auf **WPA3 (SAE)** um, oder
mindestens **WPA2 mit PMF auf _erforderlich_** (802.11w). WPA3 erzwingt geschützte
Management-Frames, gefälschte Deauth/Disassociation wird ignoriert. **Wiederhole
danach denselben Deauth-Test**  die Clients sollten verbunden bleiben, was belegt,
dass das Upgrade die Lücke geschlossen hat. Dieses Vorher/Nachher ist der Sinn:
Nutze Ereshkigal, um die WPA2 → WPA3-Migration zu begründen und zu prüfen.

> Nur gegen ein Netz, das dir gehört oder das du testen darfst, in deinem kontrollierten Labor.

## Fehlerbehebung

| Symptom | Lösung |
|---------|--------|
| **Keine COM-Ports** | USB-Seriell-Treiber installieren; ein Datenkabel (nicht nur Laden) verwenden. |
| **„Failed to open COM…"** | Ein anderes Programm belegt den Port (Serial-Monitor, anderer Flasher). Schließen. |
| **Wiederholt, dann Fehler** | Während der Wiederholung die Download-Modus-Folge ausführen: BOOT halten, RESET tippen, BOOT loslassen. |
| **Immer noch Fehler** | **Geschwindigkeit** auf `921600` senken und erneut flashen. |

## Zum Firmware-Format

`Ereshkigal.efw` ist die Firmware im eigenen Paketformat von Ereshkigal. Der Flasher
bereitet sie intern für das Board auf du entpackst nichts und brauchst keine
Zusatzwerkzeuge. Halte `.exe` und `.efw` zusammen.

---

<div align="center">
<sub>Ereshkigal von <b>Titan Digitalsoft</b> · Flasher 2.0.0 · Nur autorisierte Tests</sub>
</div>
