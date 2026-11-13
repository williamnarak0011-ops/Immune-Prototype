# Immune Colony: Art Bible (sections 1-5)

Source material: `Immune Summary.pdf`, a friend's notes and book illustrations from *Immune*.
Every figure is drawn in code in `index.html` (`SPR_PAINT` / `SPR_ANIM`). There is no emoji art,
and none of the book's art is traced or copied.

## 1. Visual identity
**"Real cell anatomy, wearing a work uniform."**
- The body comes from the biology: the outline, spikes or arms, nucleus and colour family follow the notes.
- The outfit comes from the job. A player who knows nothing about cells should still be able to say
  "the soldier", "the janitor" or "the SWAT guy".
- Each sprite has a body, eyes and an outfit. Detail goes on the head and chest, and the edges stay
  readable at play size (r ≈ 8-14 px).

## 2. Mood
Flat vector with a soft glossy highlight, set on dark, warm tissue. Cartoon eyes give each cell a
personality. Enemies get angry brows and a mask.

## 3. Shape language: every role has its own silhouette
| Role | Silhouette that tells it apart |
|---|---|
| Soldier (Neutrophil) | round, horn spikes around the bottom, helmet dome |
| Cleaner (Macrophage) | largest, lumpy amoeba, sideways cap bill |
| Courier (Dendritic) | small core with long floppy arms, flat cap, satchel |
| Bodyguard (NK) | sun-ray rim, black shades bar |
| SWAT (Killer T) | gear spikes, tall dark helmet, red zig-zag arms |
| Antibody Gunner (Plasma B) | wide oval, Y antibodies on its rim, spout on its side |
| General (Helper T) | fuzzy scalloped rim, tall peaked cap, yellow wavy arms |
| Builder (Fibroblast) | spindle / lens shape, yellow hard hat |
| Virus | ball with club spikes, black mask band, loot sack |

## 4. Colour system
- **Innate cells are warm:** pink neutrophil, orange macrophage, magenta dendritic.
- **Lymphocytes are cool:** blue Killer T, purple/blue Helper T and B cell. NK is green inside with a cyan rim.
- **Viruses** take their strain colour (`FAMILY_COLORS` A-D) on the envelope and spike knobs.
- **Role accent colours** (UI, buildings, names) must stay unique. Purple `INFECT` is reserved for
  infection, so the B-cell accent is teal even though its body is purple.
- **Deliberate deviation from the book:** infected cells are purple, not crimson, so they can't be
  confused with red Strain-A virus.
- **Colour-blind backup:** the role is always carried by the silhouette and the hat, never by colour alone.

## 5. Character direction: cast
| Unit | Body (from notes) | Uniform | Game role (from notes) |
|---|---|---|---|
| Neutrophil "Soldier Cell" | pink, horn spikes, lobed blue nucleus | army helmet, grenade belt | eats virus; careless (8% chance to hurt a nearby builder); explodes into a NET on death near virus |
| Macrophage "Cleaner Cell" | orange amoeba, yellow rim and spots, purple nucleus | janitor cap, hi-vis vest | eats virus and apoptotic bubbles; killer mode (purple glow, red nucleus, ×1.5) inside the Helper T aura |
| Dendritic "Courier Cell" | magenta, floppy arms, cyan nucleus | courier cap, satchel (glows green when carrying) | carries antigen to the lymph node |
| NK "Bodyguard Cell" | green, cyan sun rays, orange nucleus | shades, earpiece, black suit | checks MHC-I "ID"; ×2 vs `mhc_down`; shades flash on attack |
| Killer T "SWAT Cell" | blue gear spikes, navy body, red triangle nucleus, red zig-zag arms | SWAT helmet, visor, gold badge | orders apoptosis, which leaves bubbles for Cleaners |
| Plasma B "Antibody Gunner" | purple oval, red-orange nucleus, Y antibodies | goggles, bandolier of Y's | tags virus (slowed, can't infect, eaten ×2) |
| Helper T "General Cell" (building) | fuzzy blue rim, bullseye nucleus, yellow arms | peaked cap, medals | aura, faster learning, macrophage killer mode |
| Fibroblast "Builder Cell" | spindle, blue nucleus (green + blue outline under interferon) | hard hat, tool belt | builds and repairs; can be infected |
| Virion | strain-coloured envelope, blue bead capsid, orange RNA, club spikes | burglar mask, loot sack | hijacks cells |
| Lymph node (Core) | — | HQ flag with an antibody emblem | — |

Asset standard: one sprite function per key, painted at radius `r` into a cache keyed by
`key|r|state|colour`. Animated parts (arms, spikes) are drawn live under the cached image.
Visual changes are verified with screenshots in `production/qa/evidence/`.
