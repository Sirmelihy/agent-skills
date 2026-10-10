# Dark mode (§16)

Read only when the `dark-mode` decision is not `none`.

## 16. Dark mode (decision `dark-mode`)

`system`: apply the `.dark` class from `prefers-color-scheme` (e.g. next-themes with `defaultTheme="system"`).
`toggle`: the same, plus a light / dark / system switch in the account menu.

Same layering, inverted. The accent flips to near-white with black text. Alpha helpers only change values:

```css
.dark {
  --canvas: #08080A;  --background: #111113;  --panel: #17171A;  --column: #1C1C20;
  --card: #222226;    --subtle: #26262B;       --popover: #222226;
  --foreground: #F5F5F4;  --card-foreground: #F5F5F4;  --popover-foreground: #F5F5F4;
  --primary: #F5F5F4;     --primary-foreground: #0A0A0A;
  --secondary: #222226;   --secondary-foreground: #F5F5F4;
  --muted: #26262B;       --muted-foreground: #A1A1A0;  --faint: #5C5C60;
  --accent: #2A2A2F;      --accent-foreground: #F5F5F4;
  --border: rgb(255 255 255 / 0.08);  --input: rgb(255 255 255 / 0.10);  --ring: #F5F5F4;
  --sidebar: #111113;  --sidebar-foreground: #F5F5F4;
  --sidebar-primary: #F5F5F4;  --sidebar-primary-foreground: #0A0A0A;
  --sidebar-accent: rgb(255 255 255 / 0.06);  --sidebar-accent-foreground: #F5F5F4;
  --sidebar-border: rgb(255 255 255 / 0.08);  --sidebar-ring: #F5F5F4;
  --hairline: rgb(255 255 255 / 0.07);  --wash: rgb(255 255 255 / 0.06);  --track: rgb(255 255 255 / 0.12);
  --success-soft: rgb(34 197 94 / 0.15);   --success-strong: #4ADE80;
  --warning-soft: rgb(234 179 8 / 0.15);   --warning-strong: #FACC15;
  --caution-soft: rgb(249 115 22 / 0.15);  --caution-strong: #FB923C;
  --danger-soft:  rgb(239 68 68 / 0.15);   --danger-strong:  #F87171;
  --info-soft:    rgb(59 130 246 / 0.15);  --info-strong:    #60A5FA;
  --chart-1: #F5F5F4;  --chart-2: #8A8A85;  --chart-3: #4A4A4E;
}
```

Solid status badges and colored icon chips (status, operation, category) keep their fill and their black text or
icon in both themes, so they need no `dark:` variants. Neutral chips follow the theme through `bg-track` and
`text-foreground`.

