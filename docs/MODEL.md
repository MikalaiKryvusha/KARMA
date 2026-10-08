# KARMA — the model

**KARMA** — Krinik Agent Relations & Mind Approximation.

> **Status:** draft 0.2 (2026-10-08; 0.2 adds the Aims layer, §5). The layers and the loop are taken from published models and shipped games (sources at
> the end); the six traits and the seven needs are the owner's choice (2026-10-08).
> **Research behind it:** [`recon-psyche.md`](https://github.com/MikalaiKryvusha/kumm/blob/main/researches/medieval-dynasty/recon-psyche.md)
> (quotes from every source, risks, the ALMA sign trap).

## 0. The one rule

**A number lives only if something visible reads it.** Every value below names the behaviour that reads it. A value
without a reader is not added — Dwarf Fortress has 50 personality facets, and its own wiki says "many of the gameplay
effects of personality facets are as yet unknown".

## 1. State of one agent — 17 numbers and a sparse list

| Layer | Values | Range | Changes | Source |
|---|---|---|---|---|
| Character | 6 bipolar traits | −1…+1 | almost never; a breakdown may shift one | The Sims 1 sliders · Crusader Kings III opposite traits |
| Mood | Pleasure, Arousal, Dominance | −1…+1 each | every tick: pulled by emotions, drifts back to rest | Mehrabian's PAD · ALMA (Gebhard 2005) |
| Needs | 7 counters | 0…1 | decay every tick at trait-scaled rates; refilled by actions | The Sims motives |
| Stress | 1 counter | 0…400 | grows from acting against one's traits, unmet needs, bad mood; slow decay | Crusader Kings III · Dwarf Fortress |
| Relations | `like(a, b)` per known agent or group | −100…+100 | changed by events b caused for a, talk, gifts, insults | RimWorld opinion · GAMYGDALA `like` |
| Memories | a few strong facts (`hurt`, `gave`, `saved`) | — | re-fire their emotion now and then, fade with time | Dwarf Fortress re-lived memories |
| Aims | 1 dream · 1–3 milestones · ~4 wishes · ~3 fears | goals with utility −1…+1 | dream: chosen once, changed only by life events; wishes and fears: re-rolled daily | The Sims 2/3/4 · Dwarf Fortress dreams (§5) |

**Traits — six, accepted by the owner** (2026-10-08 15:38, all six of the proposed list: «почему не все шеть? выглядят
логично»). Each pole is a person; each names its readers:
- Brave ↔ Craven — resting Dominance; flee or fight; risky shortcut or safe road.
- Kind ↔ Cruel — sharing with friends, pity, robbery, insult chance.
- Outgoing ↔ Reserved — company-need decay rate; how often rumours are passed.
- Hot-tempered ↔ Calm — Arousal gain from emotions; brawl chance; breakdown threshold.
- Diligent ↔ Lazy — work speed and hours; sleep-need decay rate.
- Greedy ↔ Generous — prices, theft, gifts.

**Needs — seven, accepted by the owner** (2026-10-08 15:41: «оставляем семь»): food · water · sleep · warmth · company ·
intimacy · leisure. Leisure was the owner's addition («а как же самореализация/досуг?»); self-realization is not a need
counter — it lives in the Aims layer (dream · milestones, §5).
[AI] Readers of leisure: evening rest by the fire, talk, feasts; an empty counter slows work and adds stress (RimWorld
Recreation, The Sims Fun).[/AI]

## 2. Mood — eight named states for free

PAD octants (ALMA, Table 1): `+P+A+D` Exuberant · `+P+A−D` Dependent · `+P−A+D` Relaxed · `+P−A−D` Docile ·
`−P−A−D` Bored (depressed) · `−P−A+D` Disdainful · `−P+A−D` Anxious (afraid) · `−P+A+D` Hostile (angry).
Strength = distance from zero, cut in three: slightly · moderately · fully. Eight states × three strengths = 24 labels for
a tooltip, a rumour line or a chronicle — with no extra data.

Fear and anger differ by one axis: "anger is a dominant emotion, while fear is a submissive emotion".

**Resting mood from character.** ALMA derives it from the Big Five:
```
P = 0.21·E + 0.59·A + 0.19·S
A = 0.15·O + 0.30·A − 0.57·S
D = 0.25·O + 0.17·C + 0.60·E − 0.32·A
```
⚠️ `S` is emotional **stability** (= −Neuroticism). ALMA prints the term as "Neuroticism", which inverts its sign: with the
label as printed, a neurotic agent rests pleased and calm. The sign is checked against Mehrabian 1996, equation 4
("Emotional Stability = 0.50P − 0.55A"). KARMA's own six traits map onto P, A, D directly; this formula is kept for
projects that already store the Big Five.

## 3. Events become emotions — appraisal (GAMYGDALA)

Each role has 3–5 **goals** with a utility in −1…+1. Each event type carries a row: which goals it helps or hurts
(congruence −1…+1). The engine needs nothing else — no reaction is written per agent per event.
```
desirability(event, goal, agent) = congruence(event, goal) · utility(goal)
likelihood(goal)                 = (congruence · likelihood(event) + 1) / 2
intensity(emotion)               = |desirability · Δlikelihood(goal)|                 internal
intensity(emotion)               = |desirability · Δlikelihood(goal) · like(self, b)|  social
```
`likelihood(event)` is how much the agent believes it: **seen = 1, heard = the teller's trust** — the rumour layer.
An event caused by another agent gives anger or gratitude and moves `like` (an event that helps my goals raises my liking
of its author; one that blocks them lowers it).

The same rumour "a bear at the marsh" gives fear to a herb gatherer whose goal is safe gathering, and hope to a hunter whose
goal is game.

## 4. Emotions move mood — pull and decay (ALMA)

Each emotion is a PAD point (ALMA Table 2; e.g. Fear −0.64 / +0.60 / −0.43, Anger −0.51 / +0.59 / +0.25, Gratitude
+0.4 / +0.2 / −0.3, Joy +0.4 / +0.2 / +0.1). Active emotions form a centre weighted by intensity; the mood is **pulled**
toward it, and once past it is **pushed** further into the same octant ("a person's mood gets more intense the more
experiences the person make that are supporting this mood"). With no emotions the mood **decays** back to its resting
point. Emotions decay faster than mood.

## 5. Aims — strategy, tactics, operation

Three levels, told apart by **purpose, not by duration**; each lower level says what it serves — "…, *so that* <the level
above>" — and each is a condition that is either met or not.

| Level | What it is | How many | Born from | Example (a medieval village) |
|---|---|---|---|---|
| **Strategy — the dream** | the meaning of this life: an end state | 1 | traits + seeding memories, at coming of age (The Sims 3: "related to the traits they have"; a child who saw a death may dream of revenge) | own a smithy · be the village elder · raise a big family · grow rich · see the world · avenge my father |
| **Tactics — milestones** | intermediate goals on the way, for this stretch of life | 1–3 at a time, ~4 per dream (The Sims 4: "four milestones") | the dream + the agent's situation | save 200 coins *so that* I can buy the smithy · become journeyman *so that* the master hands over the forge |
| **Operation — wishes and fears** | what pulls right now | ~4 wishes, ~3 fears (The Sims 2: "four want slots and three fear slots") | re-rolled daily from traits, role, place, friends, season | sell the axe at the market today · fear: the bandits on the north road |

**One mechanism, not a new engine.** A dream, a milestone and a wish are §3 goals with a level and a utility (dream
≈ 0.9–1.0, milestone ≈ 0.5–0.8, wish ≈ 0.1–0.3); a **fear is a goal with negative utility**. Appraisal therefore gives
hope when a milestone draws near, disappointment when it slips, fear when a feared thing becomes likely — about one's own
life, with no extra code.

**Rules:**
1. **Nesting bonus.** An action that serves a milestone that serves the dream is worth more (The Sims 3: wishes "related
   to a Sim's lifetime wish will provide 50% more").
2. **Needs come first when urgent.** The decision layer scores needs by their urgency curve and aims by utility × nesting;
   a starving dreamer eats first.
3. **Events change plans, not the calendar.** A milestone is replanned when an event blocks it ("no plan … extends with any
   certainty beyond the first contact"); a life-shaking event (family killed, house burnt) may replace the dream itself.
4. **Distance from the dream feeds stress.** Long stalls and failed milestones add stress (§1); a fulfilled fear hits like
   The Sims 2's "aspiration failure".
5. **A realised dream marks the person.** A long-lasting strong positive emotion (The Sims 2: Platinum mood that "will decay
   very slowly") and a **reward trait** (The Sims 4); then a new dream may be chosen.
6. **Readers (§0).** The dream must change something visible: which work the agent seeks, saving instead of spending,
   moving to another village, courting, turning to crime for revenge; and a line the world can tell ("dreams of his own
   smithy").

## 6. The tick (once per game hour, over flat arrays)

1. Appraise new events the agent saw or heard (§3).
2. Pull mood by active emotions; decay mood toward rest; decay emotions (§4).
3. Decay needs at trait-scaled rates; an unmet need emits its emotion (hunger → distress, starving → fear).
4. Stress += acting against own traits + time spent in a negative octant. Crossing 100 / 200 / 300 → **breakdown**, drawn
   by weight from the menu of the current octant: Anxious → hide, flee home, refuse the risky road; Hostile → brawl, theft,
   revenge on a remembered offender; Bored → drink, idle, leave the settlement. After a breakdown — **catharsis**: a
   strong positive emotion for a few days, so there is no death spiral.
5. The decision layer (utility scoring: needs × aims × traits × mood) picks the next action. KARMA supplies the numbers;
   the game supplies the actions.
6. Once a game day: re-roll wishes and fears; check milestones (met → next one, blocked → replan); add stress for a stalled
   dream (§5).

## 7. Cost

15 floats per agent plus a sparse relation list. GAMYGDALA's authors measured appraisal for 5,000 NPCs × 5 goals × 20
beliefs at 0.816 s, single thread, 3 GHz — a worst case; an hourly tick appraises only new events.

## 8. Guards against known failures

- **Runaway behaviour** (Oblivion's Radiant AI beta, The Sims' addictive Joy Booth): vetoes in the decision layer,
  breakdown cooldowns, catharsis.
- **Invisible numbers** (§0): the reader list is the gate.
- **Tuning drift:** every constant lives in data tables (RimWorld thought rows, CK3 trait vectors), not in code.
- **The ALMA sign trap** (§2): a test case — "a neurotic agent rests unpleasant and aroused".

## Sources

- Mehrabian, A. "Analysis of the Big-five Personality Factors in Terms of the PAD Temperament Model", *Australian Journal
  of Psychology* 48(2), 1996.
- Gebhard, P. "ALMA — A Layered Model of Affect", AAMAS 2005.
- Popescu, A., Broekens, J., van Someren, M. "GAMYGDALA: an Emotion Engine for Games", *IEEE Transactions on Affective
  Computing* 5(1), 2014.
- Forbus, K., Wright, W. "Some notes on programming objects in The Sims", Northwestern University.
- RimWorld, The Sims, Crusader Kings III, Dwarf Fortress — community and official wikis (quoted in the research doc).
- Aims (§5): The Sims Wiki — "Lifetime wish", "Wish", "Wants and fears", "Aspiration (The Sims 4)"; Dwarf Fortress Wiki —
  "Personality goal"; levels by purpose and the "so that" link — military doctrine (JP 3-0, MCDP 1) and Hoshin Kanri, as
  summarised in the Unliminium project's research on strategy, tactics and operation.
