<a id="english"></a>

# Krinik's KARMA: A Psychological Model for Game AI Agents

<p align="center">
  <a href="#english"><img src="https://img.shields.io/badge/English-2C7BE5?style=for-the-badge" alt="English"></a>
  &nbsp;
  <a href="#russian"><img src="https://img.shields.io/badge/Русский-C0392B?style=for-the-badge" alt="Русский"></a>
</p>

![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-draft%200.2-orange)

**KARMA** — **K**rinik **A**gent **R**elations & **M**ind **A**pproximation.

Eighteen numbers per character that make NPCs afraid, angry, friendly, depressed, aggressive or in love — and make them
act on it. A small set of simple values and formulas; the variety comes from how they combine. Built to plug into a game's
own code and mechanics, for any game.

## Layers

| Layer | Numbers | What it drives |
|---|---|---|
| Character | 7 traits, each a pair of opposites | where mood rests, how fast needs grow, which breakdowns are possible |
| Mood | 3: pleasure · arousal · dominance | 8 named states: afraid, angry, depressed, relaxed, exuberant… |
| Needs | 7: food · water · sleep · warmth · company · intimacy · leisure | what the character goes looking for |
| Stress | 1 | breakdowns when life goes against one's nature |
| Relations | one number per acquaintance | who shares food and news, who takes revenge |
| Memories | a few strong facts | old wrongs and old kindness that flare up again |
| Aims | a dream · milestones · today's wishes and fears | strategy, tactics, operation: what the life is for, the next step towards it, what pulls right now |

Events become feelings without a script per character: each role has a few goals, each event says which goals it helps or
hurts. The same rumour of a bear near the marsh frightens the herb gatherer and gives the hunter hope. What was seen counts
in full; what was heard counts as much as the teller is trusted.

Every layer comes from a published model or a shipped game — Mehrabian's PAD, ALMA, GAMYGDALA, RimWorld, The Sims,
Crusader Kings III, Dwarf Fortress. Full specification: [docs/MODEL.md](docs/MODEL.md).

## Status

Draft 0.2: the model is specified; a reference implementation in C# comes next. First game: a living-world mod for
Medieval Dynasty.

## License

MIT © Mikalai Kryvusha (KOT KRINIK)

---

<a id="russian"></a>

# Krinik's KARMA: психологическая модель для ИИ-агентов в играх

<p align="center">
  <a href="#english"><img src="https://img.shields.io/badge/English-2C7BE5?style=for-the-badge" alt="English"></a>
  &nbsp;
  <a href="#russian"><img src="https://img.shields.io/badge/Русский-C0392B?style=for-the-badge" alt="Русский"></a>
</p>

**KARMA** — **K**rinik **A**gent **R**elations & **M**ind **A**pproximation: приближение отношений и разума агента.

Пятнадцать чисел на персонажа — и NPC пугается, злится, дружит, впадает в тоску, лезет в драку, влюбляется, а главное —
поступает так, как чувствует. Показатели и формулы простые, разнообразие рождается из их сочетания. Модель встраивается в
код и механики любой игры.

## Слои

| Слой | Чисел | Что решает |
|---|---|---|
| Характер | 7 черт, каждая — пара противоположностей | где отдыхает настроение, как быстро растут нужды, какие срывы возможны |
| Настроение | 3: удовольствие · возбуждение · власть | 8 состояний: напуган, зол, подавлен, спокоен, ликует… |
| Нужды | 7: еда · вода · сон · тепло · общение · близость · досуг | за чем человек идёт |
| Стресс | 1 | срывы, когда жизнь идёт против натуры |
| Отношения | по числу на каждого знакомого | с кем делятся едой и новостями, кому мстят |
| Память | несколько сильных фактов | старые обиды и старое добро, которые вспыхивают снова |
| Стремления | мечта · вехи · желания и страхи на сегодня | стратегия, тактика, операция: ради чего жизнь, следующий шаг к этому, что тянет прямо сейчас |

Событие становится чувством без сценария на каждого: у роли несколько целей, у события — каким целям оно помогает или
мешает. Один и тот же слух о медведе у болота пугает травницу и обнадёживает охотника. Увиденное весит полностью,
услышанное — настолько, насколько веришь рассказчику.

Каждый слой взят из опубликованной модели или выпущенной игры: PAD Мехрабиана, ALMA, GAMYGDALA, RimWorld, The Sims,
Crusader Kings III, Dwarf Fortress. Полная спецификация — [docs/MODEL.md](docs/MODEL.md).

## Состояние

Черновик 0.2: модель описана, следующая — эталонная реализация на C#. Первая игра — мод живого мира для Medieval Dynasty.

## Лицензия

MIT © Mikalai Kryvusha (KOT KRINIK)
