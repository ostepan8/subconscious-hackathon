---
theme: default
title: Agents on the Edge
info: |
  ## Agents on the Edge
  Subconscious × ACM Hackathon, Northeastern University — 2026-04-09.
  Custom Slidev deck. See DESIGN.md for provenance.
author: Owen Stepan · Subconscious Systems
date: "2026 · 04 · 09"
class: text-base
drawings:
  persist: false
transition: slide-left
mdc: true
colorSchema: dark
canvasWidth: 1920
aspectRatio: "16/9"
highlighter: shiki
lineNumbers: false
fonts:
  sans: "Manrope"
  serif: "Manrope"
  mono: "Geist Mono"
  weights: "200,300,400,500,600,700,800"
  provider: google
download: false
layout: cover
---

# Agents <em>on&nbsp;the</em> Edge.

Where prompts become production systems. A 2-hour, 15-minute sprint
to build real agents on real infrastructure — no boilerplate, no
orchestration code, no excuses.

---
layout: split
tag: WHO WE ARE
n: "02"
title: "Who We Are"
kicker: "● PLATFORM"
heading: "You write <em>prompts</em>.<br/>We handle the rest."
---

::left::

<p>
Subconscious is a developer-first platform for building
production-ready AI agents. Context management, tool
orchestration, long-horizon reasoning, and MCP support —
all handled for you.
</p>

<p>
<strong>Focus on <em style="color:var(--orange); font-style: normal;">what</em> your agent
should do.</strong> We'll take care of the <strong>how</strong>.
</p>

<div class="pills">
  <StatPill label="CONTEXT" value="128K → ∞" />
  <StatPill label="TOOLS" value="MCP · HTTP · CODE" />
  <StatPill label="REASONING" value="LONG-HORIZON" />
</div>

::right::

<ReasoningTree />

<style scoped>
.pills { display: flex; gap: 10px; margin-top: 28px; flex-wrap: wrap; }
</style>

<!--
The Subconscious platform decomposes a single high-level task
into a dynamic tree of subtasks — what we call a "trace". Each
leaf can call tools, spawn more subtasks, or return a value
that the parent uses to continue reasoning.
-->

---
layout: split
tag: TIMELINE
n: "03"
title: "How Today Works"
kicker: "● SCHEDULE"
heading: "How today <em>works</em>."
---

::left::

<ScheduleRail :slots="[
  { time: '2:15',  label: 'Presentation & Workshop', detail: 'Intro + live walkthrough' },
  { time: '2:30',  label: 'Build',                   detail: 'Solo or teams ≤ 4' },
  { time: '4:30',  label: 'Submission & Judging',    detail: 'Form on Discord' },
  { time: '4:45',  label: 'Final Presentations',     detail: '5-minute demos' },
  { time: '5:00',  label: 'Prizes',                  detail: 'Most Creative · Most Profitable' },
]" />

::right::

<div class="rules">
  <div class="rules__head">
    <span class="mono-tag">● RULES OF ENGAGEMENT</span>
  </div>

  <div class="rules__item">
    <div class="rules__num mono">01</div>
    <div>
      <div class="rules__label">Solo or teams up to four.</div>
      <div class="rules__sub">Whatever you ship has to be yours.</div>
    </div>
  </div>

  <div class="rules__item">
    <div class="rules__num mono">02</div>
    <div>
      <div class="rules__label">5 minutes to form teams.</div>
      <div class="rules__sub">Right after the workshop. Use the Discord.</div>
    </div>
  </div>

  <div class="rules__item">
    <div class="rules__num mono">03</div>
    <div>
      <div class="rules__label">2 hours to build.</div>
      <div class="rules__sub">Ship something real. Judging is ruthless.</div>
    </div>
  </div>
</div>

<style scoped>
.rules {
  display: flex;
  flex-direction: column;
  gap: 24px;
  padding: 40px 40px 44px;
  border: 1px solid var(--border);
  border-radius: 18px;
  background: var(--surface);
  box-shadow: var(--shadow-card);
}
.rules__head { margin-bottom: 8px; }
.rules__item {
  display: grid;
  grid-template-columns: 56px 1fr;
  gap: 20px;
  align-items: start;
  padding-top: 22px;
  border-top: 1px solid var(--border);
}
.rules__item:first-of-type { border-top: 0; padding-top: 0; }
.rules__num {
  font-size: 22px;
  color: var(--orange);
  font-weight: 600;
  letter-spacing: 0.02em;
}
.rules__label {
  font-family: var(--font-display);
  font-size: 26px;
  font-weight: 700;
  color: var(--text);
  line-height: 1.15;
}
.rules__sub {
  margin-top: 4px;
  font-size: 16px;
  color: var(--text-faint);
  letter-spacing: 0.02em;
}
</style>

---
layout: default
tag: SETUP
n: "04"
title: "Set-Up"
---

<div class="setup">
<div class="setup__copy">

<div class="kicker mono-tag">● STEP 01</div>

<h2>Create an <em>API key</em>.</h2>

Head to <a href="https://www.subconscious.dev/">subconscious.dev</a>, make an account, and grab an API key. You'll get <strong>$5 in credits</strong> just for signing up — enough for everything you build today.

<div class="setup__steps">
<div class="step"><span class="step__n mono">01</span><span>Sign up with GitHub or Google</span></div>
<div class="step"><span class="step__n mono">02</span><span>Land on the dashboard</span></div>
<div class="step"><span class="step__n mono">03</span><span>Open <code>API Keys</code> in the sidebar</span></div>
</div>

</div>
<div class="setup__shots">

<BrowserFrame src="/assets/platform/jump-in.png" url="subconscious.dev / dashboard" alt="dashboard" />

<BrowserFrame src="/assets/platform/playground.png" url="subconscious.dev / playground" alt="playground" />

</div>
</div>

<style scoped>
.setup {
  display: grid;
  grid-template-columns: 1.05fr 1.15fr;
  gap: 72px;
  align-items: center;
  height: 100%;
  max-height: 760px;
}
.setup__copy { align-self: center; }
.kicker { color: var(--orange); margin-bottom: 16px; display: block; }
.setup h2 {
  font-size: 76px;
  line-height: 0.98;
  letter-spacing: -0.035em;
  margin-bottom: 24px;
}
.setup h2 em { color: var(--orange); font-style: normal; }
.setup p { font-size: 20px; line-height: 1.55; color: var(--text-muted); max-width: 46ch; }

.setup__steps {
  margin-top: 24px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.step {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 14px 20px;
  border: 1px solid var(--border);
  border-radius: 10px;
  background: var(--surface);
  color: var(--text);
  font-size: 18px;
}
.step__n {
  width: 28px; height: 28px;
  display: grid; place-items: center;
  border-radius: 6px;
  background: var(--orange-wash);
  color: var(--orange);
  font-size: 12px;
  letter-spacing: 0.08em;
}
.step code {
  font-family: var(--font-mono);
  padding: 2px 8px;
  background: var(--surface-2);
  border: 1px solid var(--border);
  border-radius: 4px;
  color: var(--orange);
  font-size: 15px;
}

.setup__shots {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-height: 680px;
  overflow: hidden;
  align-self: center;
}
.setup__shots :deep(figure) { max-height: 330px; }
.setup__shots :deep(img)    { max-height: 280px; object-fit: cover; object-position: top center; }
</style>

---
layout: default
tag: SETUP
n: "05"
title: "Set-Up · Continued"
---

<div class="keymod">
<div class="keymod__head">

<div class="kicker mono-tag">● STEP 02</div>

<h2>Name it. <em>Save it.</em></h2>

Name the key something you'll recognize — <code>hackathon</code> works fine — then copy it <strong>once</strong>. We never show the full value again.

</div>
<div class="keymod__cards">

<div class="kcard">
<div class="kcard__bar"><span class="mono">Create New API Key</span><span class="kcard__x">×</span></div>
<div class="kcard__body">
<label class="mono-tag">API KEY NAME</label>
<div class="kcard__input"><span class="mono">hackathon</span><span class="caret"></span></div>
<div class="kcard__actions"><button class="btn btn--ghost">Cancel</button><button class="btn btn--primary">Create API Key</button></div>
</div>
</div>

<div class="kcard kcard--result">
<div class="kcard__bar"><span class="mono">API Key Created</span><span class="kcard__x">×</span></div>
<div class="kcard__body">
<label class="mono-tag">your new key · copy once</label>
<div class="kcard__key"><span class="mono">sk-b0f82<span class="dots">••••••••••••••••••••••••</span></span><button class="copy mono">COPY</button></div>
<div class="kcard__warn mono">● keep this secret. rotate if exposed.</div>
</div>
</div>

</div>
</div>

<style scoped>
.keymod {
  display: grid;
  grid-template-columns: 0.9fr 1.2fr;
  gap: 72px;
  align-items: center;
  height: 100%;
}
.kicker { color: var(--orange); display: block; margin-bottom: 16px; }
.keymod h2 {
  font-size: 84px;
  line-height: 1;
  letter-spacing: -0.035em;
  margin-bottom: 24px;
}
.keymod h2 em { color: var(--orange); font-style: normal; }
.keymod p {
  font-size: 22px;
  line-height: 1.55;
  color: var(--text-muted);
  max-width: 44ch;
}
.keymod code {
  font-family: var(--font-mono);
  background: var(--surface-2);
  border: 1px solid var(--border);
  padding: 2px 8px;
  border-radius: 4px;
  color: var(--orange);
  font-size: 15px;
}

.keymod__cards {
  display: flex;
  flex-direction: column;
  gap: 24px;
}
.kcard {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  box-shadow: var(--shadow-card);
  overflow: hidden;
  transform: translateY(16px);
  opacity: 0;
  animation: kcard-in 720ms var(--ease-out) forwards;
}
.kcard--result { animation-delay: 200ms; }
.kcard__bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 20px;
  border-bottom: 1px solid var(--border);
  background: var(--surface-2);
  color: var(--text);
  font-size: 14px;
}
.kcard__x { color: var(--text-faint); font-size: 18px; }
.kcard__body { padding: 24px 24px 26px; display: flex; flex-direction: column; gap: 14px; }
.kcard__body label { color: var(--text-faint); }
.kcard__input {
  padding: 14px 18px;
  background: var(--surface-2);
  border: 1px solid var(--border-hi);
  border-radius: 8px;
  display: flex;
  align-items: center;
  gap: 8px;
  color: var(--text);
  font-size: 18px;
}
.caret { display: inline-block; width: 2px; height: 18px; background: var(--orange); animation: blink 1.1s steps(1) infinite; }
.kcard__actions {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  margin-top: 6px;
}
.btn {
  padding: 12px 22px;
  border-radius: 8px;
  font-family: var(--font-mono);
  font-size: 13px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border: 1px solid transparent;
  cursor: pointer;
}
.btn--ghost { background: transparent; color: var(--text-muted); border-color: var(--border); }
.btn--primary {
  background: var(--orange);
  color: #0a0a0a;
  font-weight: 600;
  box-shadow: 0 0 0 1px var(--orange), 0 12px 28px var(--orange-glow);
}
.kcard__key {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 18px;
  background: var(--surface-2);
  border: 1px solid var(--border-hi);
  border-radius: 8px;
  font-size: 18px;
}
.kcard__key .dots { color: var(--text-faint); letter-spacing: 2px; }
.copy {
  background: transparent;
  border: 1px solid var(--border-hi);
  color: var(--orange);
  padding: 6px 12px;
  border-radius: 6px;
  font-size: 11px;
  letter-spacing: 0.1em;
  cursor: pointer;
}
.kcard__warn {
  color: var(--orange);
  font-size: 12px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  display: flex;
  align-items: center;
  gap: 8px;
}

@keyframes kcard-in { to { opacity: 1; transform: none; } }
@keyframes blink { 50% { opacity: 0; } }
</style>

---
layout: split
tag: WALKTHROUGH
n: "06"
title: "Python SDK"
kicker: "● SDK · PYTHON"
heading: "Your first agent,<br/>in <em>ten lines</em>."
---

::left::

<p>
Install the SDK, point it at your key, and give it a job. The
platform handles reasoning, tool orchestration, retries, and
memory. You hand it intent; it returns a result.
</p>

<div class="install mono">
  <span class="install__dollar">$</span>
  <span>pip install subconscious</span>
</div>

<div class="links">
  <div class="link">
    <span class="mono-tag">FULL WALKTHROUGH</span>
    <a class="mono" href="https://tinyurl.com/5bs495ym">tinyurl.com/5bs495ym</a>
  </div>
  <div class="link">
    <span class="mono-tag">PYPI</span>
    <span class="mono">subconscious · 1.x</span>
  </div>
</div>

::right::

<TokenStream
  title="agent.py — subconscious"
  :lines="[
    { text: 'from subconscious import Subconscious', kind: 'code' },
    { text: '', kind: 'code' },
    { text: '# spin up a client with your hackathon key', kind: 'comment' },
    { text: 'client = Subconscious(api_key=\u0022sk-b0f82...\u0022)', kind: 'code' },
    { text: '', kind: 'code' },
    { text: '# describe what you want, not how to do it', kind: 'comment' },
    { text: 'run = client.runs.create(', kind: 'code' },
    { text: '    prompt=\u0022Research AGI labs and summarize their bets.\u0022,', kind: 'code' },
    { text: '    tools=[\u0022web_search\u0022, \u0022python\u0022],', kind: 'code' },
    { text: ')', kind: 'code' },
    { text: '', kind: 'code' },
    { text: 'print(run.result)', kind: 'prompt' },
    { text: '→ {\u0022summary\u0022: \u0022...\u0022, \u0022sources\u0022: [..]}', kind: 'out' },
  ]"
/>

<div class="marquee-wrap">

<IntegrationMarquee />

</div>

<style scoped>
.marquee-wrap { margin-top: 24px; }
.install {
  display: inline-flex;
  align-items: center;
  gap: 14px;
  margin: 24px 0 28px;
  padding: 14px 22px;
  border: 1px solid var(--border);
  border-radius: 8px;
  background: var(--surface);
  color: var(--text);
  font-size: 20px;
}
.install__dollar { color: var(--orange); }
.links { display: grid; grid-template-columns: auto auto; gap: 32px; margin-top: 20px; }
.link { display: flex; flex-direction: column; gap: 4px; }
.link .mono-tag { color: var(--text-faint); }
.link .mono { color: var(--text); font-size: 16px; }
.link a { border-bottom: 1px solid var(--orange); color: var(--orange); }
</style>

---
layout: split
tag: DOCS
n: "07"
title: "Docs Overview"
kicker: "● REFERENCE"
heading: "Everything you<br/>need, <em>indexed</em>."
---

::left::

<p>
The docs are the source of truth. Every engine, every tool,
every run shape, every pricing detail. If you get stuck,
this is the first place you look.
</p>

<div class="docs__list">
  <div class="docs__item"><span class="mono-tag">01 · OVERVIEW</span><span>Platform architecture &amp; first run</span></div>
  <div class="docs__item"><span class="mono-tag">02 · RUNS</span><span>Create, stream, and replay traces</span></div>
  <div class="docs__item"><span class="mono-tag">03 · TOOLS</span><span>Built-ins, MCP, custom HTTP</span></div>
  <div class="docs__item"><span class="mono-tag">04 · ENGINES</span><span>Models, reasoning depth, pricing</span></div>
  <div class="docs__item"><span class="mono-tag">05 · TEMPLATES</span><span>Copy-ready starting points</span></div>
</div>

<div class="docs__link">
  <span class="mono-tag">LIVE</span>
  <a href="https://docs.subconscious.dev/overview" class="mono">docs.subconscious.dev/overview</a>
</div>

::right::

<BrowserFrame
  src="/assets/platform/templates.png"
  url="docs.subconscious.dev/overview"
  alt="Subconscious docs"
/>

<style scoped>
.docs__list {
  margin-top: 24px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.docs__item {
  display: grid;
  grid-template-columns: 180px 1fr;
  align-items: center;
  gap: 20px;
  padding: 14px 18px;
  border: 1px solid var(--border);
  border-radius: 8px;
  background: var(--surface);
  color: var(--text);
  font-size: 18px;
  transition: all var(--dur-base) var(--ease-out);
}
.docs__item:hover {
  border-color: var(--orange);
  transform: translateX(6px);
}
.docs__item .mono-tag { color: var(--orange); }
.docs__link {
  margin-top: 28px;
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 14px 20px;
  background: var(--orange-wash);
  border: 1px solid var(--orange);
  border-radius: 8px;
  color: var(--text);
}
.docs__link .mono-tag { color: var(--orange); }
.docs__link a { border-bottom: 1px solid var(--orange); color: var(--orange); font-size: 16px; }
</style>

---
layout: split
tag: INSPIRATION
n: "08"
title: "Example Agent Ideas"
kicker: "● WHAT TO BUILD"
heading: "Start with what<br/>we're <em>best at</em>."
---

::left::

<p>
Subconscious is optimized for long, messy, tool-heavy work.
If your task fits one of these shapes, you'll have a much
easier time shipping in two hours.
</p>

<div class="capabilities">
  <div class="cap">
    <span class="cap__k mono">01</span>
    <span class="cap__v">Unstructured, messy data</span>
  </div>
  <div class="cap">
    <span class="cap__k mono">02</span>
    <span class="cap__v">Workflows where the end result is known, but the path isn't</span>
  </div>
  <div class="cap">
    <span class="cap__k mono">03</span>
    <span class="cap__v">Lots of tool calling</span>
  </div>
  <div class="cap">
    <span class="cap__k mono">04</span>
    <span class="cap__v">Extreme information volume — too big for the context window</span>
  </div>
  <div class="cap">
    <span class="cap__k mono">05</span>
    <span class="cap__v">Long-running background tasks</span>
  </div>
</div>

::right::

<div class="projects">
  <div class="projects__head">
    <span class="mono-tag">● LIVE PROJECTS · BUILT ON SUBCONSCIOUS</span>
  </div>

  <a class="project" href="https://ai-agent-degree-planner.vercel.app/">
    <div class="project__num mono">01</div>
    <div>
      <div class="project__title">AI Degree Planner</div>
      <div class="project__url mono">ai-agent-degree-planner.vercel.app</div>
    </div>
  </a>

  <a class="project" href="https://resume-tailoring-agent.subconscious.dev/dashboard">
    <div class="project__num mono">02</div>
    <div>
      <div class="project__title">Resume Tailoring Agent</div>
      <div class="project__url mono">resume-tailoring-agent.subconscious.dev</div>
    </div>
  </a>

  <a class="project" href="https://subconscious-scheduler.vercel.app/">
    <div class="project__num mono">03</div>
    <div>
      <div class="project__title">School Scheduler</div>
      <div class="project__url mono">subconscious-scheduler.vercel.app</div>
    </div>
  </a>

  <a class="project" href="https://subconscious-remotion-demo.vercel.app/">
    <div class="project__num mono">04</div>
    <div>
      <div class="project__title">Remotion Video Agent</div>
      <div class="project__url mono">subconscious-remotion-demo.vercel.app</div>
    </div>
  </a>
</div>

<style scoped>
.capabilities {
  margin-top: 24px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.cap {
  display: grid;
  grid-template-columns: 44px 1fr;
  align-items: baseline;
  gap: 12px;
  padding: 12px 0;
  border-top: 1px solid var(--border);
}
.cap:first-child { border-top: 0; }
.cap__k { color: var(--orange); font-size: 13px; letter-spacing: 0.1em; }
.cap__v { color: var(--text); font-size: 18px; line-height: 1.4; }

.projects {
  padding: 28px 28px 30px;
  border: 1px solid var(--border);
  border-radius: 16px;
  background: var(--surface);
  box-shadow: var(--shadow-card);
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.projects__head { margin-bottom: 10px; }
.project {
  display: grid;
  grid-template-columns: 44px 1fr;
  gap: 18px;
  align-items: center;
  padding: 14px 16px;
  border: 1px solid transparent;
  border-radius: 10px;
  color: var(--text);
  transition: all var(--dur-base) var(--ease-out);
}
.project:hover {
  border-color: var(--border-hi);
  background: var(--surface-2);
  transform: translateX(4px);
}
.project__num { color: var(--orange); font-size: 13px; letter-spacing: 0.1em; }
.project__title {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 700;
  color: var(--text);
}
.project__url {
  font-size: 13px;
  color: var(--text-faint);
  margin-top: 2px;
  letter-spacing: 0.02em;
}
</style>

---
layout: default
tag: INSPIRATION
n: "09"
title: "Agent Ideas"
---

<div class="ideas">
  <div class="ideas__head">
    <div class="kicker mono-tag">● STARTING POINTS</div>
    <h2>Some <em>agents</em> worth building.</h2>
    <p>Ten ideas we'd fund tomorrow. Pick one, remix one, or ignore us entirely.</p>
  </div>

  <div class="ideas__grid">
    <AgentIdeaCard tag="01 · CAREERS"
      title="Resume Optimization Agent"
      body="Tailors resumes to job postings with concrete suggestions. High repeat usage across job seekers." />
    <AgentIdeaCard tag="02 · CAREERS"
      title="Job Application Autofill"
      body="Fills repetitive job forms via headless browser. Directly reduces friction in job searching." />
    <AgentIdeaCard tag="03 · GROWTH"
      title="Cold Email with Live Research"
      body="Drafts outreach after researching the recipient or company. Founders, sales reps, and recruiters want this." />
    <AgentIdeaCard tag="04 · INBOX"
      title="Inbox Triage Agent"
      body="Sorts, labels, and prioritizes incoming emails automatically. Email overload drives daily usage." />
    <AgentIdeaCard tag="05 · SOCIAL"
      title="Social Post + Visuals"
      body="Platform-specific posts with matching visuals. Content creators and founders post constantly." />
    <AgentIdeaCard tag="06 · DEVTOOLS"
      title="Bug Triage &amp; Log Analysis"
      body="Analyzes logs and error reports to identify likely causes. Developers lose massive time debugging." />
    <AgentIdeaCard tag="07 · MEMORY"
      title="Long-Term Assistant (mem0 / Zep)"
      body="Remembers preferences, goals, and past decisions. Stickiness from personalization and memory." />
    <AgentIdeaCard tag="08 · EDU"
      title="Study Guide Generator"
      body="Converts lecture notes and slides into structured study guides. Students reuse every exam cycle." />
    <AgentIdeaCard tag="09 · CAREERS"
      title="Interview Prep Agent"
      body="Generates role-specific questions and talking points. Job seekers prep repeatedly." />
    <AgentIdeaCard tag="10 · SALES"
      title="Company Profile Builder"
      body="Produces internal briefs from public company data. Sales, recruiting, investing workflows." />
  </div>
</div>

<style scoped>
.ideas { height: 100%; display: flex; flex-direction: column; gap: 34px; }
.ideas__head .kicker { color: var(--orange); margin-bottom: 10px; display: block; }
.ideas__head h2 {
  font-size: 76px;
  line-height: 1;
  letter-spacing: -0.035em;
  margin-bottom: 10px;
}
.ideas__head h2 em { color: var(--orange); font-style: normal; }
.ideas__head p { font-size: 20px; color: var(--text-muted); max-width: 70ch; }
.ideas__grid {
  flex: 1;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-template-rows: 1fr 1fr;
  gap: 16px;
}
</style>

---
layout: default
tag: JUDGING
n: "10"
title: "Judging Criteria"
---

<div class="judging">
  <div class="judging__head">
    <div class="kicker mono-tag">● HOW YOU WIN</div>
    <h2>Two ways to <em>take home</em> a prize.</h2>
    <p>Creativity for the builders with nothing to lose. Profitability for the builders with everything to prove.</p>
  </div>

  <div class="judging__cards">
    <JudgingCard
      eyebrow="● CATEGORY 01"
      weight="50%"
      title="Most Creative."
      body="The most out-of-the-box, unexpected, delightful use case. Go weird. Go small. Go niche. Surprise us."
      icon="brain"
    />
    <JudgingCard
      eyebrow="● CATEGORY 02"
      weight="50%"
      title="Most Profitable."
      body="Most likely to become a real-world product. Tangible audience, plausible pricing, solves a real pain."
      icon="money"
    />
  </div>
</div>

<style scoped>
.judging { height: 100%; display: flex; flex-direction: column; gap: 44px; }
.judging__head .kicker { color: var(--orange); display: block; margin-bottom: 12px; }
.judging__head h2 {
  font-size: 88px;
  line-height: 0.98;
  letter-spacing: -0.035em;
  margin-bottom: 16px;
}
.judging__head h2 em { color: var(--orange); font-style: normal; }
.judging__head p { font-size: 22px; color: var(--text-muted); max-width: 70ch; }
.judging__cards {
  flex: 1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
}
</style>

---
layout: centered
tag: RUBRIC
n: "11"
title: "Rubric"
---

<div class="rubric">
  <div class="kicker mono-tag">● SCORING · JUDGES VIEW</div>
  <h2>The <em>rubric</em>.</h2>
  <p>Four axes. Equal weight. Written by the same people who score you.</p>

  <div class="rubric__grid">
    <div class="rubric__col">
      <div class="axis">
        <span class="axis__k mono">01</span>
        <div>
          <div class="axis__t">Technical Execution</div>
          <div class="axis__s">Does it run? Does it run well?</div>
        </div>
      </div>
      <div class="axis">
        <span class="axis__k mono">02</span>
        <div>
          <div class="axis__t">Use of Subconscious</div>
          <div class="axis__s">Leveraging the platform's strengths</div>
        </div>
      </div>
      <div class="axis">
        <span class="axis__k mono">03</span>
        <div>
          <div class="axis__t">Creativity</div>
          <div class="axis__s">Would we have thought of this?</div>
        </div>
      </div>
      <div class="axis">
        <span class="axis__k mono">04</span>
        <div>
          <div class="axis__t">Market Viability</div>
          <div class="axis__s">Could you charge for this?</div>
        </div>
      </div>
    </div>

<div class="rubric__qr">

<QRBlock data="https://tinyurl.com/2dxvjuun" caption="Full rubric" />

</div>
  </div>
</div>

<style scoped>
.rubric { display: flex; flex-direction: column; align-items: center; gap: 20px; }
.rubric .kicker { color: var(--orange); margin-bottom: 4px; }
.rubric h2 { font-size: 92px; line-height: 1; margin: 0; }
.rubric h2 em { color: var(--orange); font-style: normal; }
.rubric p { font-size: 22px; color: var(--text-muted); margin: 8px 0 24px; }
.rubric__grid {
  display: grid;
  grid-template-columns: 1.1fr 1fr;
  gap: 72px;
  align-items: center;
  text-align: left;
  max-width: 1300px;
}
.rubric__col { display: flex; flex-direction: column; gap: 18px; }
.axis {
  display: grid;
  grid-template-columns: 44px 1fr;
  gap: 18px;
  padding: 18px 22px;
  border: 1px solid var(--border);
  border-radius: 12px;
  background: var(--surface);
  align-items: baseline;
}
.axis__k { color: var(--orange); font-size: 13px; letter-spacing: 0.1em; }
.axis__t { font-family: var(--font-display); font-size: 22px; font-weight: 700; color: var(--text); }
.axis__s { font-size: 14px; color: var(--text-faint); margin-top: 4px; }
</style>

---
layout: section
tag: BUILD
n: "12"
title: "Build!"
---

<h2>Build<em>.</em></h2>

<p>Clock's ticking. Hands up if you need help — we'll be circling the room.</p>

<div class="build__strip">
  <StatPill label="DURATION" value="2H 00M" />
  <StatPill label="TEAMS" value="SOLO → 4" />
  <StatPill label="TARGET" value="ONE WORKING AGENT" />
</div>

<style scoped>
.build__strip {
  display: flex;
  gap: 16px;
  margin-top: 24px;
  animation: fade-in 900ms var(--ease-out) 800ms backwards;
}
@keyframes fade-in { from { opacity: 0; transform: translateY(10px); } }
</style>

---
layout: split
tag: SUBMISSION
n: "13"
title: "Group Submission"
kicker: "● WHEN TIME IS UP"
heading: "How to <em>turn in</em><br/>your project."
---

::left::

<p>
Drop your submission in the form below. Same link lives on the
hackathon Discord. Four fields, one minute, done.
</p>

<div class="submit__list">
  <div class="submit__row">
    <span class="submit__k mono">01</span>
    <div>
      <div class="submit__t">Name(s)</div>
      <div class="submit__s">Everyone on the team. GitHub handles are fine.</div>
    </div>
  </div>
  <div class="submit__row">
    <span class="submit__k mono">02</span>
    <div>
      <div class="submit__t">Project name &amp; description</div>
      <div class="submit__s">One sentence. Tell us what it does.</div>
    </div>
  </div>
  <div class="submit__row">
    <span class="submit__k mono">03</span>
    <div>
      <div class="submit__t">GitHub link</div>
      <div class="submit__s">Public repo, or add <code>@subconscious-systems</code>.</div>
    </div>
  </div>
  <div class="submit__row">
    <span class="submit__k mono">04</span>
    <div>
      <div class="submit__t">Slideshow of your project</div>
      <div class="submit__s">Slides, Notion, Figma — whatever you can screen-share.</div>
    </div>
  </div>
</div>

::right::

<QRBlock
  data="https://forms.gle/Qvoo3TuX92SJK1oJ9"
  caption="Submission form · also on Discord"
/>

<style scoped>
.submit__list {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 26px;
}
.submit__row {
  display: grid;
  grid-template-columns: 44px 1fr;
  gap: 18px;
  align-items: start;
  padding: 16px 20px;
  border: 1px solid var(--border);
  border-radius: 12px;
  background: var(--surface);
}
.submit__k { color: var(--orange); font-size: 13px; letter-spacing: 0.1em; }
.submit__t { font-family: var(--font-display); font-size: 22px; font-weight: 700; color: var(--text); }
.submit__s { font-size: 15px; color: var(--text-faint); margin-top: 4px; }
.submit__s code {
  font-family: var(--font-mono);
  padding: 2px 6px;
  background: var(--surface-2);
  border: 1px solid var(--border);
  border-radius: 4px;
  color: var(--orange);
  font-size: 12px;
}
</style>

---
layout: section
tag: DEMOS
n: "14"
title: "Demos"
---

<h2>Demos<em>.</em></h2>

<p>Time's up. Let's see what you built.<br/>Five minutes per team. No slides required.</p>

<div class="demos__timer">
  <div class="timer__ring"></div>
  <div class="timer__label mono">5:00 PER TEAM · NO SLIDES NEEDED</div>
</div>

<style scoped>
.demos__timer {
  display: flex;
  align-items: center;
  gap: 18px;
  margin-top: 32px;
  opacity: 0;
  animation: in 900ms var(--ease-out) 700ms forwards;
}
.timer__ring {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--orange);
  box-shadow: 0 0 0 4px rgba(255, 92, 40, 0.18), 0 0 24px var(--orange-glow);
  animation: pulse 1.8s var(--ease-in-out) infinite;
}
.timer__label {
  color: var(--text-faint);
  letter-spacing: 0.18em;
}
@keyframes in    { to { opacity: 1; } }
@keyframes pulse {
  0%, 100% { transform: scale(1);   opacity: 1;   }
  50%      { transform: scale(1.4); opacity: 0.4; }
}
</style>

---
layout: split
tag: FEEDBACK
n: "15"
title: "Feedback"
kicker: "● ONE LAST THING"
heading: "Tell us what<br/>we <em>got wrong</em>."
---

::left::

<p>
We're shipping Subconscious fast. Your honest feedback is the
only way the next hackathon beats this one. Three questions,
live on Discord too.
</p>

<div class="feedback__list">
  <div class="feedback__row">
    <span class="feedback__k mono">01</span>
    <div>
      <div class="feedback__t">Your name</div>
      <div class="feedback__s">So we can thank you.</div>
    </div>
  </div>
  <div class="feedback__row">
    <span class="feedback__k mono">02</span>
    <div>
      <div class="feedback__t">What did the platform do well?</div>
      <div class="feedback__s">The features that unblocked you.</div>
    </div>
  </div>
  <div class="feedback__row">
    <span class="feedback__k mono">03</span>
    <div>
      <div class="feedback__t">What did you wish it had?</div>
      <div class="feedback__s">Be mean. It helps.</div>
    </div>
  </div>
</div>

::right::

<QRBlock
  data="https://forms.gle/R4GANtqcCAVsThHc7"
  caption="Feedback form · also on Discord"
/>

<style scoped>
.feedback__list {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 26px;
}
.feedback__row {
  display: grid;
  grid-template-columns: 44px 1fr;
  gap: 18px;
  padding: 16px 20px;
  border: 1px solid var(--border);
  border-radius: 12px;
  background: var(--surface);
}
.feedback__k { color: var(--orange); font-size: 13px; letter-spacing: 0.1em; }
.feedback__t { font-family: var(--font-display); font-size: 22px; font-weight: 700; color: var(--text); }
.feedback__s { font-size: 15px; color: var(--text-faint); margin-top: 4px; }
</style>
