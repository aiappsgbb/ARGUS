---
agent: 'agent'
model:
  - Claude Opus 4.6 (copilot)
  - Claude Sonnet 4 (copilot)
tools: ['githubRepo', 'search/codebase', 'edit', 'changes', 'runCommands']
description: 'Generate a professional PPTX pitch deck about this repository for sellers and presales engineers'
---

# Generate Pitch Deck

Create a polished, professional PowerPoint (PPTX) presentation about this repository. The deck is for **sellers and presales engineers** to pitch the solution to customers and stakeholders. The tone is **business-first** — lead with impact, follow with the demo story, keep tech details brief.

## Phase 1 — Research & Analysis

Before creating any slides, deeply analyze the repository in this order:

### 1A. Business Context (do this FIRST)
1. **Read `.github/ip-metadata.json`** — this is your primary source of truth. Extract:
   - `name` and `description` → slide titles and taglines
   - `industry` → tailor the narrative to this vertical (e.g., "Financial Services" → compliance, risk, fraud; "Healthcare" → patient outcomes, regulatory)
   - `pattern` → map each pattern to a business capability (e.g., "AI/ML" → intelligent automation, "Data & Analytics" → data-driven decisions)
   - `services` → Azure platform story (which Azure services power the solution)
   - `maturity` → set expectations (Gold = production-ready, Silver = validated, Bronze = early)
   - `region` → geographic relevance
   - `owner` and `contacts` → closing slide attribution
   - `tags` → keywords for positioning
   - `version`, `createdDate`, `lastUpdated` → maturity signals
2. **Read README.md** — extract the value proposition, key features, prerequisites, and deployment steps
3. **Research business impact** — based on the industry, patterns, and services identified, reason about:
   - What **customer pain points** does this solve? Think about real-world business problems, not technical ones
   - What **measurable outcomes** can customers expect? (time to market, cost reduction, operational efficiency, new capabilities)
   - What **competitive advantage** does the Azure-native approach provide vs. alternatives?
   - What **industry trends** make this solution timely and relevant?

### 1B. Technical Context (supporting detail only)
4. **Scan `/docs` folder** (if present) — pull in architecture descriptions, user guides, demo walkthroughs
5. **Read `azure.yaml`** (if present) — understand services, infrastructure, deployment model
6. **Scan `/infra` folder** (if present) — identify Azure services used (from Bicep/Terraform)
7. **Scan `/src` folder structure** — understand the tech stack, languages, frameworks
8. **Look for demo assets** — screenshots, architecture diagrams in `/assets`, `/docs`, or `/images`
9. **Understand the user flow** — trace how an end-user would interact with the tool from start to finish. Look at UI components, API endpoints, CLI commands, or any entry points. Build a mental model of the demo story.

Compile your findings into a structured brief before proceeding to slide creation.

## Phase 2 — Slide Deck Structure (15–20 slides max)

Build the deck with this structure. The **business story comes first**, then the **demo walkthrough**, then brief **tech details**. Adapt section lengths based on available content — skip sections that don't apply, but never exceed 20 slides.

### Section 1: Opening & Business Context (4–6 slides)
- **Title slide** — Solution name (from `ip-metadata.json` `name`), one-line tagline (from `description`), date, "Confidential — Microsoft Internal". Include maturity badge and industry tag
- **Agenda** — Visual agenda with icons, not a plain numbered list. Use a horizontal timeline or card layout
- **The Problem** — Frame as a business problem the customer faces. Use industry-specific language from `ip-metadata.json` `industry`. Be concrete: "Enterprises in [industry] struggle with [pain point] leading to [business impact]"
- **Why Now** — Industry trends, market drivers, competitive pressure that make this timely. Connect the patterns from `ip-metadata.json` to real market needs
- **The Opportunity** — Quantify the opportunity where possible. What does solving this unlock for the customer? Frame outcomes: faster time-to-market, reduced costs, new revenue streams, better compliance posture
- **Use Cases** — 2–3 concrete customer scenarios. Tailor to the `industry` field. Each use case should be a short narrative (who, what problem, what outcome), not just a title

### Section 2: Solution & Demo Walkthrough (4–6 slides)
- **Solution Overview** — 2–3 sentence elevator pitch + 3 key differentiators. Use a visual layout: large icon or illustration on the left, text on the right
- **Key Capabilities** — 3–5 headline capabilities with one-line descriptions. Use an icon grid layout (2×2 or 3×2) instead of bullet lists when there are few items
- **Demo Walkthrough** — This is critical. Walk through how a user would actually USE the tool step-by-step:
  1. How does the user get started? (setup, login, first screen)
  2. What is the primary workflow? (the main thing the tool does)
  3. What does the user see at each step? (describe UI screens, CLI output, or API responses)
  4. What is the "wow moment"? (the key value the user gets)
  - Use numbered steps with brief descriptions. If screenshots exist in the repo, reference them.
  - If the tool has a web UI, describe the page flow. If it's a CLI tool, show the command sequence. If it's an API, show the request/response pattern.
- **Customer Outcomes** — Measurable results: time saved, cost reduced, capability unlocked, risk mitigated. Use a visual metric layout (big numbers with labels) rather than bullets

### Section 3: Technical Overview (2–3 slides — keep it brief)
- **Architecture at a Glance** — ONE slide. High-level architecture showing Azure services and data flow. If an architecture image exists in the repo, reference it. Otherwise create a clean text-based component diagram. List Azure services from `ip-metadata.json` `services` with their roles
- **Deployment & Getting Started** — ONE slide. 3–5 steps to deploy (derived from README). Prerequisites. Include `azd up` if applicable. Keep it actionable
- **Security & Integration** — ONE slide, only if relevant. Auth model, networking, integration points. Skip if the repo doesn't have significant security patterns

### Section 4: Closing (1–2 slides)
- **Resources & Next Steps** — Clear call-to-action. Link to repo, documentation. Quick-start command. What should the audience do next?
- **Thank You / Q&A** — Use details from `ip-metadata.json`:
  - Solution name and version (from `name`, `version`)
  - Owner and contacts (from `owner`, `contacts.technical`, `contacts.business`) — format as "@alias" Microsoft aliases
  - Repository URL (from `repository.url`)
  - Industry and patterns (from `industry`, `pattern`) as tags
  - Maturity level (from `maturity`) and last updated date (from `lastUpdated`)

## Phase 3 — PPTX File Creation

Use the `python-pptx` library to create the actual `.pptx` file. Follow these visual design guidelines:

### Visual Standards
- **Color palette**: Use Microsoft brand-adjacent colors:
  - Primary: `#0078D4` (Microsoft Blue)
  - Secondary: `#50E6FF` (Light Azure Blue)
  - Accent: `#00B294` (Teal Green)
  - Dark: `#243A5E` (Dark Navy) for backgrounds on title/section dividers
  - Text: `#323130` (near-black) on white, `#FFFFFF` on dark backgrounds
- **Fonts**: Use `Segoe UI` for both headings and body — available on all Windows machines
- **Slide dimensions**: Widescreen 16:9 (13.33" × 7.5")
- **Margins**: At least 0.5" on all sides
- **Font sizes**:
  - Slide titles: 28–32pt bold
  - Subtitles: 18–20pt
  - Body text: 14–16pt
  - Footnotes/captions: 10–12pt

### Layout Rules — Professional Polish
- **Max 5 bullet points per slide** — if more content, split across slides
- **No walls of text** — use short phrases, not sentences
- **Adaptive layouts based on content density**:
  - **1–3 items**: Use a **card/icon grid** layout — large icons with centered text blocks, evenly spaced across the slide. Do NOT use a lonely bullet list floating in whitespace
  - **4–5 items**: Use a **two-column layout** or **icon grid** (2×3 or 2×2 with description)
  - **6+ items**: Split across multiple slides or use a compact table
  - **Metrics/numbers**: Use a **big number layout** — large font number (36–44pt bold) with a small label below (12–14pt). Arrange 2–4 metrics in a row across the slide
  - **Comparisons**: Use side-by-side columns with contrasting header colors (before/after, traditional vs. this solution)
  - **Process/workflow**: Use a **horizontal step flow** — numbered circles connected by arrows with brief labels
- **Section divider slides** — dark navy (`#243A5E`) background with large white text, used between the 3 major sections
- **Footer on every content slide**: solution name on left, "Microsoft Confidential" on right, slide number centered
- **Consistent alignment** — use the same text box positions across similar slide types. Title always at the same Y position. Content area always starts at the same Y position
- **White space is good** — don't fill every pixel. Let content breathe. A slide with 3 well-spaced cards looks far more professional than 3 bullets crammed at the top

### Implementation Steps
1. Install python-pptx: `pip install python-pptx`
2. Create the presentation programmatically
3. Save as `PITCH_DECK.pptx` in the repository root
4. Commit the file

## Required Deliverable

You **MUST** create a file named `PITCH_DECK.pptx` in the root of the repository containing the complete presentation.

## Quality Checklist

Before finalizing, verify:
- [ ] Deck has 15–20 slides (no more, no fewer than 12)
- [ ] Title slide has solution name and tagline derived from `ip-metadata.json`
- [ ] Business value leads — first half of the deck is non-technical
- [ ] Demo walkthrough is concrete and step-by-step, not abstract
- [ ] Architecture section is ONE slide, accurately reflecting actual Azure services
- [ ] No placeholder text remains (e.g., "[INSERT HERE]")
- [ ] All bullet points are concise (≤12 words each)
- [ ] Slides with few items use card/grid layouts, NOT lonely bullet lists
- [ ] Color scheme is consistent throughout
- [ ] Footer appears on all content slides
- [ ] Closing slide includes contacts, repo URL, and metadata from `ip-metadata.json`
- [ ] File is saved as `PITCH_DECK.pptx` in repo root
- [ ] Content is factual — derived from actual repo contents, not hallucinated
