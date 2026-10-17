# Accessibility basics for Roblox UI and gameplay

Treat these as a checklist for screens and flows you build; verify behaviors in Studio's device emulation and on real devices where possible.

- **Contrast and size:** text and icons must stay legible on small phones and over busy 3D backgrounds; avoid conveying meaning by color alone (add an icon, shape or label); keep tap targets large enough for touch.
- **Text:** support longer strings (localization), avoid text baked into images, respect the player's text-size preference where the platform exposes one (verify the current GuiService settings in the docs).
- **Motion and effects:** keep screen shake, flashing and fast camera moves moderate; provide a reduce-motion or effects toggle for strong effects; never flash rapidly.
- **Input:** every action reachable by touch, mouse/keyboard and gamepad; visible focus for gamepad navigation; no hold-only or precision-only requirements without an alternative.
- **Audio:** do not rely on sound alone for critical information; provide separate music/effects volume and a mute option.
- **Cognitive load:** short instructions, one new mechanic at a time ([onboarding](../onboarding-retention-ux.md)), clear cause and effect, undo or confirm for destructive or paid actions.
- **Safety for young players:** clear price and odds before purchase ([reward design](../reward-design-random-items.md)), no hidden or misleading controls.
