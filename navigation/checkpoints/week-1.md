---
layout: post
title: Week 1 Quest Log
description: Sprint 1, Week 1 checkpoint, turned into a playable quest log with the real code runners wired up.
permalink: /checkpoints/week-1
codemirror: true
search_exclude: true
toc: true
---

<style>
.wk1-intro {
  padding: 18px 22px;
  border-radius: 12px;
  border: 1px solid var(--ui-border, #444);
  background: var(--panel, rgba(127,127,127,0.08));
  margin-bottom: 24px;
}
.wk1-board {
  width: 100%;
  border-collapse: collapse;
  margin: 16px 0 28px;
  font-size: 0.95em;
}
.wk1-board th, .wk1-board td {
  border: 1px solid var(--ui-border, #444);
  padding: 8px 12px;
  text-align: left;
}
.wk1-board th {
  background: var(--panel, rgba(127,127,127,0.12));
}
.wk1-quest {
  border: 1px solid var(--ui-border, #444);
  border-left: 5px solid var(--pref-accent-color, #7c5cff);
  border-radius: 10px;
  padding: 18px 22px;
  margin: 28px 0;
  background: var(--panel, rgba(127,127,127,0.04));
}
.wk1-quest.boss {
  border-left-color: #e53935;
}
.wk1-quest-head {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 10px;
  margin-bottom: 8px;
}
.wk1-quest-head h2 { margin: 0; }
.wk1-chip {
  display: inline-block;
  padding: 3px 10px;
  border-radius: 999px;
  font-size: 0.75em;
  font-weight: 700;
  background: var(--pref-accent-color, #7c5cff);
  color: #fff;
  white-space: nowrap;
}
.wk1-chip.boss { background: #e53935; }
.wk1-stars { letter-spacing: 2px; opacity: 0.85; }
.wk1-flavor {
  font-style: italic;
  opacity: 0.85;
  margin: 4px 0 14px;
}
.wk1-xpbar {
  height: 8px;
  border-radius: 6px;
  background: var(--ui-border, #444);
  overflow: hidden;
  margin: 18px 0 6px;
}
.wk1-xpbar-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--pref-accent-color, #7c5cff), #45b7d1);
}
</style>

<div class="wk1-intro" markdown="1">
**Sprint 1 — Week 1 Quest Log.** The checkpoint, turned into something worth opening again: eight quests, each worth XP, and the code runners below are the *real* interactive components — not screenshots. Run them, break them, fix them, right here.
</div>

## 🗺️ Quest Board

| # | Quest | Difficulty | XP | Type |
|---|-------|:----------:|:--:|------|
| 1 | Code Runners — Raw MD | ★☆☆ | 100 | Multi-language runner |
| 2 | UI Runner | ★★☆ | 100 | Canvas / DOM runner |
| 3 | Game Runner Examples | ★★★ 👑 | 150 | **Boss fight** — GameEngine |
| 4 | Code Runner - Java | ★★☆ | 100 | Java runner |
| 5 | Code Runner - JavaScript | ★☆☆ | 100 | JS runner |
| 6 | Student Engagement | ★☆☆ | 100 | Lore / grading rules |
| 7 | Fullstack Development | ★★☆ | 100 | Design thinking |
| 8 | CSA MCQ Lessons | ★★★ 👑 | 150 | **Boss fight** — practice gauntlet |

**Total XP this week: 900** — clear all 8 for Sprint 1 mastery.

<div class="wk1-xpbar"><div class="wk1-xpbar-fill" style="width: 100%;"></div></div>
*(bar shows quests documented, not yet completed — that part's still pending)*

---

<div class="wk1-quest" markdown="1">
<div class="wk1-quest-head"><h2>🧩 Quest 1 — Code Runners: Raw MD</h2><span class="wk1-chip">100 XP</span><span class="wk1-stars">★☆☆</span></div>
<p class="wk1-flavor">A single page, four languages, zero mercy. Fix each snippet to clear the room.</p>

One page, multiple code runners — Python, Java, and JavaScript side by side, each with its own broken snippet to fix. This is the "raw markdown" pattern: no notebook conversion, just `{% raw %}{% include runners/code.html %}{% endraw %}` called directly with captured `challenge` and `code` variables.

**Objective A — Python: fix the missing parenthesis**

{% capture wk1_cr_challenge_a %}
This print statement is one character away from working. Find it and close the call.
{% endcapture %}

{% capture wk1_cr_code_a %}
print('Hello World'
{% endcapture %}

{% include runners/code.html
   runner_id="wk1-cr-a"
   language="python"
   challenge=wk1_cr_challenge_a
   code=wk1_cr_code_a
%}

**Objective B — Java: fix the compilation error**

{% capture wk1_cr_challenge_b %}
The compiler's throwing an error again. One missing symbol at the end of the println line — track it down.
{% endcapture %}

{% capture wk1_cr_code_b %}
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello, Java")
  }
}
{% endcapture %}

{% include runners/code.html
   runner_id="wk1-cr-b"
   language="java"
   challenge=wk1_cr_challenge_b
   code=wk1_cr_code_b
%}

*Params for building a new one: `runner_id` (required, unique per page), `language` (python / java / javascript), `challenge`, `code`, `height` (default 300px).*
</div>

<div class="wk1-quest" markdown="1">
<div class="wk1-quest-head"><h2>🎨 Quest 2 — UI Runner</h2><span class="wk1-chip">100 XP</span><span class="wk1-stars">★★☆</span></div>
<p class="wk1-flavor">Trade `print()` for pixels. Everything renders straight into <code>outputElement</code>.</p>

Same `challenge` / `code` / `runner_id` pattern as Code Runner, except the code gets a live `outputElement` div to draw into — canvas, DOM nodes, whatever gets built.

**Objective A — draw a canvas square**

{% capture wk1_ui_challenge_a %}
Warm-up: get a 200x200 red square centered on a 400x400 canvas. This is the "hello world" of the UI Runner.
{% endcapture %}

{% capture wk1_ui_code_a %}
outputElement.innerHTML = '';
const canvas = document.createElement('canvas');
canvas.width = 400;
canvas.height = 400;
outputElement.appendChild(canvas);
const ctx = canvas.getContext('2d');
ctx.fillStyle = 'red';
ctx.fillRect(100, 100, 200, 200);
{% endcapture %}

{% include runners/ui.html
   runner_id="wk1-ui-a"
   challenge=wk1_ui_challenge_a
   code=wk1_ui_code_a
%}

**Objective B — an interactive button**

{% capture wk1_ui_challenge_b %}
DOM manipulation check: build a button that toggles color on click. Click it a few times — that's the whole test.
{% endcapture %}

{% capture wk1_ui_code_b %}
outputElement.innerHTML = '';
const button = document.createElement('button');
button.textContent = 'Click Me!';
button.style.padding = '20px 40px';
button.style.fontSize = '18px';
button.style.border = 'none';
button.style.borderRadius = '8px';
button.style.cursor = 'pointer';
button.style.backgroundColor = '#3b82f6';
button.style.color = 'white';
let isBlue = true;
button.addEventListener('click', () => {
    button.style.backgroundColor = isBlue ? '#ef4444' : '#3b82f6';
    button.textContent = isBlue ? 'Red!' : 'Blue!';
    isBlue = !isBlue;
});
outputElement.appendChild(button);
{% endcapture %}

{% include runners/ui.html
   runner_id="wk1-ui-b"
   challenge=wk1_ui_challenge_b
   code=wk1_ui_code_b
   height="250px"
%}

*Progression: DOM basics → canvas drawing → animation → full game logic.*
</div>

<div class="wk1-quest boss" markdown="1">
<div class="wk1-quest-head"><h2>👑 Quest 3 — Game Runner Examples (BOSS)</h2><span class="wk1-chip boss">150 XP</span><span class="wk1-stars">★★★</span></div>
<p class="wk1-flavor">The big one this week. Real GameEngine, real sprite, real WASD movement — no simulation.</p>

The code has to export a `GameControl` class plus a `gameLevelClasses` array; the runner builds the canvas, Start/Pause/Stop/Reset controls, and a level selector around it automatically.

**Boss objective — background + custom player**

{% capture wk1_game_challenge_a %}
Hit Start and walk the character around the desert with WASD or the arrow keys. Custom level, custom sprite, custom rules.
{% endcapture %}

{% capture wk1_game_code_a %}
import GameControl from '/assets/js/GameEnginev1/essentials/GameControl.js';
import GameEnvBackground from '/assets/js/GameEnginev1/essentials/GameEnvBackground.js';
import Player from '/assets/js/GameEnginev1/essentials/Player.js';

class CustomLevel {
  constructor(gameEnv) {
    const path = gameEnv.path;
    const bgData = {
        name: 'custom_bg',
        src: path + "/images/gamebuilder/bg/clouds.jpg",
        pixels: { height: 720, width: 1280 }
    };
    const playerData = {
      id: 'Hero',
      src: path + "/images/gamify/chillguy.png",
      SCALE_FACTOR: 5,
      STEP_FACTOR: 1000,
      ANIMATION_RATE: 50,
      INIT_POSITION: { x: 100, y: 300 },
      pixels: { height: 512, width: 384 },
      orientation: { rows: 4, columns: 3 },
      down: { row: 0, start: 0, columns: 3 },
      downRight: { row: 1, start: 0, columns: 3, rotate: Math.PI/16 },
      downLeft: { row: 2, start: 0, columns: 3, rotate: -Math.PI/16 },
      right: { row: 1, start: 0, columns: 3 },
      left: { row: 2, start: 0, columns: 3 },
      up: { row: 3, start: 0, columns: 3 },
      upRight: { row: 1, start: 0, columns: 3, rotate: -Math.PI/16 },
      upLeft: { row: 2, start: 0, columns: 3, rotate: Math.PI/16 },
      hitbox: { widthPercentage: 0.45, heightPercentage: 0.2 },
      keypress: { up: 87, left: 65, down: 83, right: 68 }
    };
    this.classes = [
      { class: GameEnvBackground, data: bgData },
      { class: Player, data: playerData },
    ];
  }
}
export const gameLevelClasses = [CustomLevel];
export { GameControl };
{% endcapture %}

{% include runners/game.html
   runner_id="wk1-game-a"
   challenge=wk1_game_challenge_a
   code=wk1_game_code_a
   height="420px"
%}

*Controls: WASD / arrows to move, E or Enter to interact with NPCs, Esc to pause. Troubleshooting note: if the canvas is blank, it's almost always an import path or a missing export.*
</div>

<div class="wk1-quest" markdown="1">
<div class="wk1-quest-head"><h2>☕ Quest 4 — Code Runner: Java</h2><span class="wk1-chip">100 XP</span><span class="wk1-stars">★★☆</span></div>
<p class="wk1-flavor">Notebook-native. This one started life as a Jupyter cell, not raw markdown.</p>

Generated straight from a Jupyter notebook — tag the code cell with `// CODE_RUNNER: <challenge text>`, keep `codemirror: true` in the frontmatter, and `make` builds the runner automatically. No duplicated code between the notebook and the site.

**Objective — `indexOf` and `substring` in the wild**

{% capture wk1_java_challenge %}
Trace through shortenMessage() for four different inputs and predict the output before hitting run.
{% endcapture %}

{% capture wk1_java_code %}
public class Main {
    private String shortenMessage(String message, String str) {
        int position = message.indexOf(str);
        int length = str.length();
        if (position == -1) {
            return message;
        }
        String newFront = message.substring(0, position);
        String newBack = message.substring(position + length);
        return (newFront + newBack);
    }

    public void driver() {
        String[][] messageData = {
            {"Hello, OpenCS!", ","},
            {"Java code code coding!", "Java"},
            {"Java programming is fun.", "."},
            {"No substring here", "exception"},
        };
        for (String[] data : messageData) {
            System.out.println("Shortened Message: " + shortenMessage(data[0], data[1]));
        }
    }

    public static void main(String[] args) {
        new Main().driver();
    }
}
{% endcapture %}

{% include runners/code.html
   runner_id="wk1-java-a"
   language="java"
   challenge=wk1_java_challenge
   code=wk1_java_code
   height="380px"
%}
</div>

<div class="wk1-quest" markdown="1">
<div class="wk1-quest-head"><h2>📜 Quest 5 — Code Runner: JavaScript</h2><span class="wk1-chip">100 XP</span><span class="wk1-stars">★☆☆</span></div>
<p class="wk1-flavor">Same notebook pipeline as the Java quest, just swap <code>%%js</code> for the language cell magic.</p>

**Objective A — personalize the record**

{% capture wk1_js_challenge_a %}
Swap in a different name and age. Small win, but a clean one.
{% endcapture %}

{% capture wk1_js_code_a %}
const person = {
    name: "Jane",
    age: 16
};
console.log(person);
{% endcapture %}

{% include runners/code.html
   runner_id="wk1-js-a"
   language="javascript"
   challenge=wk1_js_challenge_a
   code=wk1_js_code_a
%}

**Objective B — complete the loop**

{% capture wk1_js_challenge_b %}
Print 1 through 5. Two blanks, one loop — don't overthink it.
{% endcapture %}

{% capture wk1_js_code_b %}
for (let i = ???; i <= ???; i++) {
  console.log(i);
}
{% endcapture %}

{% include runners/code.html
   runner_id="wk1-js-b"
   language="javascript"
   challenge=wk1_js_challenge_b
   code=wk1_js_code_b
%}

*Build note: `make` scans for `CODE_RUNNER` comments, pulls the challenge text out, strips the magic command, clears the notebook's own output, and injects the runner block — no manual sync required.*
</div>

<div class="wk1-quest" markdown="1">
<div class="wk1-quest-head"><h2>📈 Quest 6 — Student Engagement</h2><span class="wk1-chip">100 XP</span><span class="wk1-stars">★☆☆</span></div>
<p class="wk1-flavor">The lore behind how grading actually works — worth knowing before going deep into Sprint 1.</p>

The CSA course runs 9 sprints across weeks 0–37: Java onboarding → full-stack web dev → team projects → AP exam prep → final project. Engagement is tracked through individual issues/blogs, team issues, and regular checkpoint reviews — which is exactly what this page *is*.

**Quest objectives (the actual grading rules):**
- [ ] Split time roughly **60% team goals / 40% individual mastery**
- [ ] Keep individual issues + blog posts current — the personal learning trail
- [ ] Show up in team issues so collaborative progress is visible
- [ ] Hit checkpoint reviews and demos on schedule

**XP tiers that map to real grades:** 55% minimum → 75% effort demonstrated → 85% complete work → 90% mastery level. Weekly score is `(points × 2) ÷ 10`.

**Evaluation categories:** Team Evaluation (3 pts: checkpoints, frontend planning, backend planning) + Individual Mastery (2 pts: technical + soft skills — code reviews, teaching participation, debugging, tool use like the browser inspector and Postman).
</div>

<div class="wk1-quest" markdown="1">
<div class="wk1-quest-head"><h2>🏗️ Quest 7 — Fullstack Development</h2><span class="wk1-chip">100 XP</span><span class="wk1-stars">★★☆</span></div>
<p class="wk1-flavor">Finn Carpenter's framing, useful for any project: front end, back end, database, API.</p>

Full stack = a feature spanning **Frontend** (what the user sees/clicks), **Backend** (server logic + database calls), **Database** (where the data lives), and **API** (how frontend and backend actually talk).

**Two questions to answer before building anything:**
1. What **data** needs to be stored, and what **endpoints** does this feature need?
2. What will the **wireframe** look like, and how does it get auto-generated?

**Worked example — an announcement feature:**
- Data: ID, author, title, body, time, tags
- Endpoints beyond CRUD: fetch by author, fetch by tag
- Wireframe: search/filter, newest announcements at the top

> The honest barrier to fullstack work is just *how much* there is to know — APIs, endpoints, wireframes, all at once. The fix isn't "know it all first," it's starting from a GitHub issue outline, following the sequence (POJO → JPA → API), and building Postman checks for GET/POST/PUT/DELETE. The JavaScript frontend isn't even a new pattern — it's the same shape as Python/Flask: design the form, format the JSON response.
</div>

<div class="wk1-quest boss" markdown="1">
<div class="wk1-quest-head"><h2>👑 Quest 8 — CSA MCQ Lessons (BOSS)</h2><span class="wk1-chip boss">150 XP</span><span class="wk1-stars">★★★</span></div>
<p class="wk1-flavor">The gauntlet. Four units, forty-eight sub-lessons, four unit quizzes standing between here and mastery.</p>

**The map:**

| Unit | Sub-lessons | Boss |
|------|:-----------:|------|
| Unit 1 | 1.1 – 1.15 | Unit 1 Quiz |
| Unit 2 | 2.1 – 2.12 | Unit 2 Quiz |
| Unit 3 | 3.1 – 3.9 | Unit 3 Quiz |
| Unit 4 | 4.1 – 4.12 | Unit 4 Quiz |

**Clear condition:** every sub-lesson checked off, all four unit quizzes passed. This is the long-haul quest — chip away at one unit per sitting instead of trying to one-shot it.
</div>

---

**Session total if everything above is cleared: 900 XP.** Next stop: Week 2.
