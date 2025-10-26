# Weyland-Yutani Dashboard Enhancements

Optional `card-mod` and layout snippets for advanced users who want to fully match the *Weyland CRT* aesthetic.

---

## Nostromo Console Card (Blinking Cursor)
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

