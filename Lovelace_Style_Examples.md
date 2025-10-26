# Weyland-Yutani Dashboard Enhancements

Optional `card-mod` and layout snippets for advanced users who want to fully match the *Weyland CRT* aesthetic.

---

### Nostromo Console Card (Blinking Cursor)

```yaml
type: markdown
entity_id: sensor.time
content: |
  USCSS NOSTROMO  |  MISSION: 180924  |  CREW: 2  |  STATUS: NORMAL
card_mod:
  style: |
    ha-card {
      --g: var(--nostromo-green, #00ff7a);
      background: transparent;
      border: none;
      padding: 8px 12px;
      font-family: var(--nostromo-font, ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace);
      color: var(--g);
      letter-spacing: 2px;
      font-size: 23px !important;
    }

    @keyframes nostromo-blink { 0%,49% { opacity: 1 } 50%,100% { opacity: 0 } }

    ha-card .markdown-content::after {
      content: "▌";
      display: inline-block;
      margin-left: 4px;
      color: var(--g);
      animation: nostromo-blink 1s steps(1,end) infinite;
    }

### Transparent Cards for Scanline Effect

card_mod:
  style: |
    ha-card {
      --g: var(--nostromo-green, #00ff7a);
      background: transparent;
      border: none;
      padding: 8px 12px;
      font-size: 20px !important;
      font-family: var(--nostromo-font, ui-monospace, Menlo, Consolas, monospace);
    }

### Weyland Logo Integration

card_mod:
  style: |
    ha-card {
      --g: var(--nostromo-green, #00ff7a);
      --a: var(--nostromo-amber, #ffb000);
      background: transparent;
      border: none;
      padding: 0;
      font-family: var(--nostromo-font, ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace);
      color: var(--g);
    }

### Thermostat Display

# A stylized horizontal thermostat display using button-card and mod-card.
# Adjust entity IDs and temperature sensors as needed.

type: custom:mod-card
grid_options:
  columns: 12
  rows: 3
card_mod:
  style: |
    ha-card {
      --nostromo-g: var(--nostromo-green, #26d665);
      --nostromo-font: var(--nostromo-font, ui-monospace, Menlo, Consolas, monospace);

      /* Scaling and sizing */
      --strip-height: 145px;
      --digit-size: 105px;
      --ambient-size: 28px;
      --btn-w: 66px;
      --btn-h: 48px;
      --rail-alpha: .30;

      width: 100%;
      height: 100%;
      background: transparent;
      border: none;
      padding: 0;
    }

    ha-card > * { position: relative; }
    ha-card > *::before,
    ha-card > *::after {
      content: "";
      position: absolute;
      left: 0; right: 0;
      height: 2px;
      background: color-mix(in srgb, var(--nostromo-g) calc(var(--rail-alpha)*100%), transparent);
      filter: drop-shadow(0 0 0.35rem color-mix(in srgb, var(--nostromo-g) 35%, transparent));
      pointer-events: none;
    }
    ha-card > *::before { top: 0; }
    ha-card > *::after  { bottom: 0; }

card:
  type: horizontal-stack
  cards:
    - type: custom:button-card
      entity: climate.hallway
      show_icon: false
      show_name: false
      show_state: false
      tap_action: none
      styles:
        card:
          - height: 80px
          - background: transparent
          - border: none
          - box-shadow: none
          - padding: 12px 18px
          - font-family: var(--nostromo-font)
          - color: var(--nostromo-g)
          - letter-spacing: 2px
          - font-size: var(--ambient-size)
          - display: flex
          - align-items: center
          - justify-content: center
          - min-width: 180px
          - border-right: 1px solid rgba(38,214,101,.28)
      custom_fields:
        ambient: |
          [[[
            const tNow = entity.attributes.current_temperature ?? states['sensor.hallway_temperature']?.state;
            const hum  = states['sensor.hallway_humidity']?.state ?? entity.attributes.humidity;
            const t    = (tNow != null && !isNaN(tNow)) ? Math.round(Number(tNow)) + '°' : '--°';
            const h    = (hum  != null && !isNaN(hum )) ? Math.round(Number(hum )) + '%' : '--%';
            return `${t} · ${h}`;
          ]]]

### Toggle Button Example

type: button
entity: switch.aerotower_power
name: AEROTOWER FAN
show_name: true
show_icon: false
show_state: false
tap_action:
  action: toggle
card_mod:
  style: |
    ha-card {
      --g: var(--nostromo-green, #00ff7a);
      --a: var(--nostromo-amber, #ffb000);
      background: transparent;
      border: 1px solid rgba(0,255,122,0.18);
      padding: 8px 12px;
      font-family: var(--nostromo-font, ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace);
      color: var(--g);
      letter-spacing: 1.5px;
      font-size: 20px !important;
    }

### Notes

# All snippets are intended for use with the Weyland CRT Theme for Home Assistant.
# They use the same color variables, typefaces, and spacing conventions for visual consistency.

