# Knaeckebrot Split Keyboard

Ein drahtloses split Keyboard mit 60 Tasten (30 pro Hälfte) basierend auf ZMK Firmware.

## Hardware

- **Controller**: Nice Nano v2 (beide Hälften)
- **Layout**: 60 Tasten total (30 pro Seite)
  - 3 Reihen mit 7 Tasten
  - 1 Reihe mit 6 Tasten  
  - 1 Reihe mit 3 Tasten (Daumentasten)
- **Verbindung**: Bluetooth zwischen Hälften und Computer

## Pin-Belegung

### Reihen (Rows)
- Row 0: GPIO 20
- Row 1: GPIO 19  
- Row 2: GPIO 18
- Row 3: GPIO 17
- Row 4: GPIO 16

### Spalten (Columns)
- Col 0: GPIO 6
- Col 1: GPIO 7
- Col 2: GPIO 8
- Col 3: GPIO 9
- Col 4: GPIO 10
- Col 5: GPIO 11
- Col 6: GPIO 12

## Keymap

### Layer 0 (Default)
Standard QWERTY Layout mit Zahlenreihe

### Layer 1 (Function)
Funktionstasten F1-F12 und Pfeiltasten

### Layer 2 (Symbol)
Symbole und Sonderzeichen

### Layer 3 (Adjust)
Bluetooth-Management und System-Funktionen

## Firmware Build

Die Firmware wird automatisch über GitHub Actions gebaut. Nach jedem Push werden die `.uf2` Dateien als Artifacts bereitgestellt.

### Manuelle Build-Anweisungen

```bash
# West Workspace initialisieren
west init -l config
west update

# Linke Hälfte bauen
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=knaeckebrot_left -DZMK_CONFIG="$(pwd)/config"

# Rechte Hälfte bauen
west build --pristine -s zmk/app -b nice_nano_v2 -- -DSHIELD=knaeckebrot_right -DZMK_CONFIG="$(pwd)/config"
```

## Installation

1. Nice Nano v2 in Bootloader-Modus versetzen
2. Entsprechende `.uf2` Datei auf das USB-Laufwerk kopieren
3. Controller startet automatisch neu

## Bluetooth Pairing

1. Linke Hälfte einschalten (wird als Master fungieren)
2. Rechte Hälfte einschalten (verbindet sich automatisch mit der linken)
3. Am Computer nach "Knaeckebrot" suchen und pairen

## Battery Management

- Automatischer Sleep-Modus nach 30 Minuten Inaktivität
- Optimierte Energieeinstellungen für lange Batterielaufzeit
- Bluetooth-Transmit-Power auf +8dBm für stabile Verbindung