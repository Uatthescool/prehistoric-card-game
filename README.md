# Prehistoric Card Game demo

Playable local-hotseat implementation of Revision 2.0 with three independently selectable 40-card singleton decks: Deck 1 Theropod Predators, Deck 2 Herbivore Development, and Deck 3 Aquatic Carnivores.

## Release contract

- Canonical decks: Deck 1 and Deck 3 each contain 22 Creatures and 18 Supports; Deck 2 contains 23 Creatures and 17 Supports.
- Sources of truth: `app/card-register.json` supplies Deck 1, shared Tag definitions, and the accepted-change ledger; `app/deck-2.ts` and `app/deck-3.ts` supply the other decks' unique records and new Supports.
- Rules engine: `app/game-engine.ts` owns deterministic state transitions and is exercised by 90 engine tests.
- Interface: `app/page.tsx` provides setup, the read-only **Inspect Deck** browser, strict click-to-pin card inspection, private hotseat handoff, game actions, projected Hunt resolution, the permanent card-inspection sidewall, and the opening-page **Learn Something** Lesson experience.
- Presentation: every full Creature and Support card reserves the same exact 23:13 artwork slot. Production artwork is used when available; newly playable cards without final art use the deliberate pending treatment.
- Lesson content: `app/lessons.ts` stores the structured Lesson states, glossary, Evidence, sources, and internal scientific-review date. The first complete vertical slice is the single-card Amargasaurus Lesson.

The authoritative continuity set for this checkpoint is:

1. `Prehistoric_Card_Game_Final_40_Card_Changes_Register.docx` — exact card records and locked implementation rulings.
2. `Prehistoric_Card_Game_Player_Rulebook_Draft_1.0.docx` — player procedure and terminology.
3. `Prehistoric_Card_Game_Design_Ledger_Draft_1.0.docx` — design principles, rationale, release history, interface contract, and open work.

When a rule changes, update the canonical register and engine tests in the same pass, then regenerate all three documents. Do not allow software-only wording to become an undocumented rule.

## Revision 2.0 highlights

- Changes Spinal Sail to protect Victory Level from Event and Tag decreases only, with the word “each” explicit in the final wording.
- Makes printed Aquatic a closed override ecosystem. An occupied Aquatic card supplies Taxon—or Tag when the base Taxa already match—while an occupied Semi-Aquatic card supplies Tag to an incoming Aquatic or Semi-Aquatic card. Semi-Aquatic remains an unrestricted bridge and counts as Aquatic for Events and Concepts, but not Adaptations.
- Makes Diet matching directional: incoming Omnivores match every Diet, incoming Carnivores match Carnivore or Omnivore, and incoming Herbivores match only Herbivore.
- Removes Piscivore as a Diet, moves all former Piscivores to Carnivore, and restores normal equal-Level or +1-Level Aquatic override progression.
- Suppresses Tropical Biodiversity when Cambrian Explosion creates a multi-draw Start Phase.
- Lets Genetic Drift's mandatory discard resolve before its five card-by-card draw animations begin.
- Reimplements Charge as same-turn Battle permission that ignores Diet only in the facing Niche and permanently lane-locks that Creature's Hunts.
- Branches Sovereign by Diet: every bearer counts as Gigantic and receives Battle protection; Carnivore/Omnivore bearers gain Territorial, while Herbivores receive Victory protection.
- Adds Deck 2 as a complete selectable Herbivore/board-development deck, including Dreadnoughtus as its exceptional Level 4 capstone.
- Adds Armament, Herd, Nesting, Bastion, Deimatic, Graviportal, Overreach, Osteoderm, and the Resonance placeholder to the active Tag registry.
- Implements Air Sacs, Thagomizer, Dental Battery, Facultative Quadrupedality, Genetic Mutations, and the board-wide counter-clockwise Stampede sequence.
- Makes Deck 3 selectable and playable with its complete 22-Creature, 18-Support singleton manifest.
- Implements Visual, Engulf, Filter Feeder, Dermal Armor, and Durophagy; Shearing Bite and Retention remain explicit placeholders.
- Adds Drought, Island Dwarfism, and the instantaneous Geological Boundary Event with their finalized board and timing rules.
- Updates Tyrannosaurus rex from placeholder Osteophagy to Durophagy; Sovereign continues to grant Gigantic and Territorial.

## Local verification

Prerequisite: Node.js `>=22.13.0` on Linux.

```bash
npm run lint
npm test
```

`npm test` runs 90 engine tests, the production build and artifact validation, and the rendered-interface checks. For interactive development, use `npm run dev`.

## Project map

| Path | Purpose |
| --- | --- |
| `app/card-register.json` | Canonical Deck 1 register and shared rules ledger |
| `app/deck-2.ts` | Canonical Deck 2 creature and new-Support records |
| `app/deck-3.ts` | Canonical Deck 3 creature and new-Support records |
| `app/game-data.ts` | Typed exports and UI-facing derived data |
| `app/game-engine.ts` | State model, legality checks, actions, and resolution |
| `app/lessons.ts` | Structured Learn Something Lessons, glossary definitions, Evidence, and sources |
| `app/page.tsx` | Interactive hotseat playtest surface |
| `app/globals.css` | Board, card, inspector, and responsive styling |
| `tests/game-engine.test.ts` | Revision 2.0 rules-engine coverage |
| `tests/rendered-html.test.mjs` | Built-page metadata and content checks |

Checkpoint deployments are immutable continuity milestones. Continue later work from the latest verified source revision.
