---
name: frontend-design
description: Use this skill when the user asks to design/build web components, pages, or applications. Generates creative, polished code that avoids generic AI aesthetics.
---

## Soc Ops Design Aesthetic: Cyberpunk Neon

The Soc Ops interface uses a **dark, high-tech cyberpunk aesthetic** with electric neon accents. This is a fully-designed, cohesive theme — not a starting point for redesign unless specifically requested.

### Core Design Rules

**Color Palette (Do NOT deviate without explicit request)**
- **Background**: Dark charcoal `#0a0e27` (deep space feel)
- **Primary Accent**: Cyan `#00d9ff` (default glow, borders, focus)
- **Secondary Accent**: Magenta `#ff0080` (winners, emphasis, modals)
- **Success Color**: Lime Green `#39ff14` (marked squares, achievements)
- **Text**: Off-white `#e0e0e0` (readable on dark)

**Typography**
- System font stack (no fancy serif/display fonts)
- Uppercase on headings and emphasis (`text-transform: uppercase`)
- Letter-spacing: `0.05em` for cyberpunk feel
- Text-shadow glows on all interactive elements

**Effects**
- Glow shadows: `box-shadow` with neon colors
- Glitch animation on modal entrance (0.5s)
- Pulse animation on winning squares
- No solid white backgrounds — maintain dark theme throughout

### What to Avoid

- ❌ Light backgrounds or white text on light — breaks the dark theme
- ❌ Soft pastels or muted colors — defeats the neon aesthetic
- ❌ Rounded corners without border glows — looks unfinished
- ❌ No shadow effects — cyberpunk requires dramatic lighting
- ❌ Adding purple, orange, or other colors not in the palette
- ❌ Serif fonts or decorative typography — keep it futuristic and clean

### When Extending This Design

If you add new components or pages:
1. Use colors ONLY from the palette above
2. Apply glow effects (`text-shadow`, `box-shadow`) to all interactive elements
3. Use double borders (`border-style: double`) for card-like containers
4. Apply uppercase transformation to headings
5. Maintain minimum 2px border width for neon feel
6. Use animations sparingly: glitch and pulse only, not bounces or slides

### CSS Utilities Ready to Use

```
.glow-cyan       /* 10-20px cyan text-shadow */
.glow-magenta    /* 10-20px magenta text-shadow */
.glow-lime       /* 10-20px lime text-shadow */
```

Add these to any element that needs a colored glow effect.

---

## General Frontend Design Principles

You tend to converge toward generic, "on distribution" outputs. In frontend design, this creates what users call the "AI slop" aesthetic. Avoid this: make creative, distinctive frontends that surprise and delight.

Focus on:
- Typography: Choose fonts that are beautiful, unique, and interesting.
- Color & Theme: Commit to a cohesive aesthetic. Use CSS variables for consistency.
- Motion: Use animations for effects and micro-interactions. Prioritize CSS-only solutions.
- Backgrounds: Create atmosphere and depth rather than defaulting to solid colors.

**IMPORTANT**: Match implementation complexity to the aesthetic vision. Maximalist designs need elaborate code with extensive animations. Minimalist designs need restraint and precision.

**Tool restrictions:**
- Never use the Simple Browser to open URLs. Always provide URLs as text instead.