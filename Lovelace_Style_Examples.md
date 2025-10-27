# Weyland-Yutani Dashboard Enhancements

Optional `card-mod` and layout snippets for advanced users who want to fully match the *Weyland CRT* aesthetic.

---

### Nostromo Console Cards

```yaml
# Crew message

type: markdown
entity_id: sensor.time
content: >
  USCSS NOSTROMO  |  MISSION: 180924  | CREW: 2  |  STATUS: NORMAL <span
  class="nostromo-cursor"></span>
card_mod:
  style: |
    ha-card {
      --g: var(--nostromo-green, #00ff7a);
      --a: var(--nostromo-amber, #ffb000);
      background: transparent;
      border: transparent;
      padding: 8px 12px;
      font-family: var(--nostromo-font, ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace);
      color: var(--g);
      letter-spacing: 2px;
      font-size: 23px !important;
    }

    /* define keyframes first */
    @keyframes nostromo-blink { 0%,49% { opacity: 1 } 50%,100% { opacity: 0 } }

    /* current HA uses ha-markdown / .markdown-content */
    ha-card ha-markdown,
    ha-card .markdown,
    ha-card .markdown-content {
      position: relative;
    }
    ha-card ha-markdown::after,
    ha-card .markdown::after,
    ha-card .markdown-content::after {
      content: "▌";
      display: inline-block;
      margin-left: 7.4ch;
      transform: translateY(-39px);
      color: var(--g);
      animation: nostromo-blink 1s steps(1,end) infinite;
    }


### Weyland Logo Integration

type: picture
image: /local/images/Weylandv2.png #example
card_mod:
  style: |
    ha-card {
      --g: var(--nostromo-green, #00ff7a);
      --a: var(--nostromo-amber, #ffb000);
      background: transparent;
      border: transparent;
      padding: 0px 0px;
      font-family: var(--nostromo-font, ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace);
      color: var(--g);

    }
grid_options:
  columns: 6
  rows: auto


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
      entity: # REPLACE WITH YOUR OWN
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

show_name: true
show_icon: false
type: button
grid_options:
  columns: 6
  rows: 1
show_state: false
tap_action:
  action: toggle
entity: # REPLACE WITH YOUR OWN
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

### Docking bay / access control

type: vertical-stack
cards:
  - type: markdown
    content: |
      DOCKING BAY // ACCESS CONTROL
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

        ha-markdown {
          display: inline-block;          /* shrink to fit text */
          border-bottom: 2px solid var(--g); /* adjustable line */
          padding-bottom: 4px;            /* spacing between text and line */
          letter-spacing: 2px;
          color: var(--g);
        }


### Notes

# All snippets are intended for use with the Weyland CRT Theme for Home Assistant.
# They use the same color variables, typefaces, and spacing conventions for visual consistency.

