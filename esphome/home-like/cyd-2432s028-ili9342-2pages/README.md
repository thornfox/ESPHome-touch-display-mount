# CYD (ESP32-2432S028R, ILI9342) – Two-Page Tile UI

Variant of the `home-like` tile UI for the Cheap Yellow Display with an **ILI9342** controller, extended to **two pages with swipe navigation**.

## What is different from `cyd-2432s028/home-like.yaml`

- **Two LVGL pages, 11 tiles** – page 1 (tiles 1–6), page 2 (tiles 7–11). Swipe left/right to switch pages (`MOVE_LEFT` / `MOVE_RIGHT`, 250 ms).
- **No accidental taps while swiping** – the swipe handler calls `lv_indev_wait_release()`, so the release after a swipe is not treated as a click on the tile under your finger. Tiles use `gesture_bubble: true` so swipes started on a tile reach the page.
- **Overlays moved to `top_layer`** – brightness slider, color/temperature picker, climate overlay, dim/wake overlay and the confirm dialog work on both pages.
- **Clock on both pages**, separate header text per page (`ROOM_NAME`, `ROOM_NAME_2`).
- **ILI9342 / 0° preset active** (landscape, USB on the right, RGB color order).
- **`buffer_size: 25%`** for the LVGL draw buffer – recommended for ESP32 boards without PSRAM; avoids the failed 153600-byte allocation on boot.
- German UI texts (`UI_*` substitutions).

The tile entities in the file are an example setup. Change the `TILE1_…` to `TILE11_…` substitutions to your own Home Assistant entities.

## Requirements

- ESPHome **2026.9.0** or newer (validated with 2026.9.1)
- `secrets.yaml` with `wifi_ssid`, `wifi_password`, `wifi_ap_password`, `smartdisplay_api_key` (see `../../secrets.yaml.example`)
- In Home Assistant: ESPHome integration → device options → enable **“Allow the device to perform Home Assistant actions”**

## Display shows garbage or wrong colors?

If the picture is rotated, only half drawn and red/blue are swapped, your board has a different controller than the active preset. Switch between the **ILI9341** and **ILI9342** presets in the `DISPLAY / ORIENTATION PRESETS` block.

---

# CYD (ESP32-2432S028R, ILI9342) – Kachel-Oberfläche mit zwei Seiten

Variante der `home-like`-Kacheloberfläche für das Cheap Yellow Display mit **ILI9342**-Controller, erweitert auf **zwei Seiten mit Wischnavigation**.

## Unterschiede zu `cyd-2432s028/home-like.yaml`

- **Zwei LVGL-Seiten, 11 Kacheln** – Seite 1 (Kacheln 1–6), Seite 2 (Kacheln 7–11). Wischen nach links/rechts wechselt die Seite (`MOVE_LEFT` / `MOVE_RIGHT`, 250 ms).
- **Kein versehentliches Schalten beim Wischen** – der Wisch-Handler ruft `lv_indev_wait_release()` auf, dadurch zählt das Loslassen nach einer Wischgeste nicht als Klick auf die Kachel darunter. Die Kacheln haben `gesture_bubble: true`, damit Wischgesten auch auf einer Kachel bei der Seite ankommen.
- **Overlays liegen im `top_layer`** – Helligkeitsregler, Farb-/Farbtemperaturwahl, Klima-Overlay, Dimm-/Weck-Overlay und Bestätigungsdialog funktionieren auf beiden Seiten.
- **Uhrzeit auf beiden Seiten**, eigene Überschrift pro Seite (`ROOM_NAME`, `ROOM_NAME_2`).
- **Preset ILI9342 / 0° aktiv** (Querformat, USB rechts, Farbreihenfolge RGB).
- **`buffer_size: 25%`** für den LVGL-Zeichenpuffer – empfohlen für ESP32 ohne PSRAM; verhindert die fehlgeschlagene 153600-Byte-Allokation beim Start.
- Deutsche Oberflächentexte (`UI_*`-Substitutions).

Die Entitäten in der Datei sind ein Beispiel-Setup. Passe die Substitutions `TILE1_…` bis `TILE11_…` an deine eigenen Home-Assistant-Entitäten an.

## Voraussetzungen

- ESPHome **2026.9.0** oder neuer (geprüft mit 2026.9.1)
- `secrets.yaml` mit `wifi_ssid`, `wifi_password`, `wifi_ap_password`, `smartdisplay_api_key` (siehe `../../secrets.yaml.example`)
- In Home Assistant: ESPHome-Integration → Geräteoptionen → **„Erlaube dem Gerät, Home-Assistant-Aktionen durchzuführen“** aktivieren

## Bild verrauscht oder falsche Farben?

Ist das Bild gedreht, nur halb gezeichnet und sind Rot und Blau vertauscht, hat dein Board einen anderen Controller als das aktive Preset. Wechsle im Block `DISPLAY / ORIENTATION PRESETS` zwischen den Presets **ILI9341** und **ILI9342**.

---

Based on / Basiert auf [akuehlewind/ESPHome-touch-display-mount](https://github.com/akuehlewind/ESPHome-touch-display-mount) (MIT License). Variant by ThornFox.
