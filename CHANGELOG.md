# Changelog

All notable changes to Career Helper are documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versions follow [Semantic Versioning](https://semver.org/).

---

## [1.9.0] - 2026-03-21

### Added
- **Wellbeing and emotional awareness in Tim's coaching** — Tim now reads emotional signals during intake, acknowledges difficulty before routing to skills, and checks in after emotionally demanding work
  - Intake Q2 branches based on emotional context: forced change gets "how are you feeling?", steady situations get "what would help most?"
  - Wellbeing Notes in preferences file carry emotional context across sessions
  - CHECK-IN line in checkpoints after skills that touch rejection, ageism, redundancy, or difficult feelings
  - Pace line in Progress Tracker after emotionally demanding sessions
  - Skill dispatch now passes emotional context to sub-agents so they can calibrate tone
- **Agent memory for Tim** (`memory: project`) — Tim now builds persistent coaching knowledge across sessions
  - Stores routing patterns, skill sequencing insights, and coaching approaches that work
  - Separate from user data (which stays in preferences file)
- **Interview Master: peer development questions** — explicit "How have you helped your colleagues improve?" question type with STAR guidance focused on the other person's outcome
- **Interview Master: company selection criteria** — "What matters most when choosing your next company?" with values-alignment answer framework
- **Wellbeing-aware checkpoint template** (Variation D) with CHECK-IN rules and concrete example

### Changed
- **Accessibility: traffic-light terminology replaced** — all references to "traffic-light indicators" changed to "text-label ratings (GREEN/AMBER/RED)" across employer-footprint SKILL.md, dashboard template, digital-footprint-audit, deep-research-reflection, and getting-the-best guide
- Dashboard template score key now includes accessibility note: "Ratings always use text labels alongside scores — never colour alone"
- Tim's "What Tim never does" lists deduplicated — Persona section covers voice/tone, Wellbeing section covers coaching boundaries, with cross-reference
- Sequencing Logic updated to require emotional acknowledgment before routing
- Returning user instructions broken into readable sub-bullets
- Mock interview hiring manager typical questions expanded with peer development and company selection criteria
- Plugin version bumped to 1.9.0

---

## [1.8.3] - 2026-03-17

### Added
- **Accessibility support across all skills and commands** — previously only Tim checked for accessibility preferences; now every skill and command does
  - All 10 non-Tim skills check for `career-helper-preferences.md` at skill start and apply dyslexia-friendly and colour-blind safe formatting
  - Skills invoked directly (not via Tim) ask once about accessibility preferences if no preferences file exists, then save for future sessions
  - `/career-helper:quick-start` includes accessibility as part of its intake questions
  - `/career-helper:status` respects accessibility preferences in its output formatting
  - Skill-specific accessibility guidance: risk matrices, dashboards, and status indicators always use text labels, never colour alone

### Changed
- README updated to reflect accessibility coverage across all skills
- Plugin version bumped to 1.8.3

---

## [1.8.0] - 2026-03-16

### Added
- **Tim — Career Coach** (`/career-helper:career-coach`) - Guided career coaching that orchestrates skills for you
  - Semi-autonomous skill orchestration — Tim understands your situation and runs the right skills in the right order
  - Structured checkpoints between skills using labelled DONE/SAVED/FLAG/NEXT format
  - Non-deterministic sequencing — adapts based on your goals, urgency, flags, and emotional signals
  - Session persistence via `career-helper-preferences.md` with consent-gated storage
  - Accessibility support: dyslexia-friendly enhanced mode (signposting, numbered options, confirmation checks, no idioms, one decision per message)
  - Colour-blind safe communication — all status conveyed through labels and words, never colour alone
  - Returning user detection with privacy-safe identity confirmation before displaying personal data
  - Error handling for skill failures with clear reporting and user choice
  - Supportive coach persona — warm, encouraging, direct, never sycophantic
- New command: `/career-helper:career-coach` to launch Tim
- New skill: `tim` with 3 reference files (routing guide, dyslexia guide, checkpoint templates)

### Changed
- `/career-helper:help` updated with Tim in skill table and routing
- `/career-helper:quick-start` mentions Tim as guided alternative at handoff
- Plugin description updated to mention guided coaching
- Plugin version bumped to 1.8.0 (11 skills including Tim)

---

## [1.7.0] - 2026-03-03

### Added
- **Non-Linear Career Explorer** - New capability (Capability 3) in Career Transitions skill
  - Comprehensive exploration of alternatives to traditional career progression
  - **Entrepreneurship:** Business readiness assessment, honest pros/cons, legal structures by region (UK/US), funding sources, financial modelling, failure rate data
  - **Startup founding:** VC vs bootstrapping comparison, funding paths (pre-seed to Series B+), co-founder dynamics, accelerator guidance, realistic success/failure rates (90% failure rate cited), equity and dilution considerations
  - **Public sector careers:** Private-to-public transition guide, Success Profiles framework, Civil Service values, salary/benefits comparison, transferable skills mapping, application tips
  - **Charity and non-profit:** Career paths (management, fundraising, programme delivery, policy, social enterprise, impact investing, grant making), "passion tax" reality, sector resources
  - **Intrapreneurship:** Organisational readiness assessment, internal venture pitching framework, pros/cons vs external entrepreneurship
  - **Multi-role skilling:** Skill stacking strategy, unique intersection identification, deliberate career episode design, hybrid career models
  - Financial readiness assessment with regional guidance
  - Transferable skills audit with meta-skills identification
  - Weighted decision matrix with reversibility assessment
  - Career narrative development (30-second, 2-minute, LinkedIn, and interview versions)
  - Research-driven with WebSearch for current data on success rates, salary benchmarks, and sector insights
- New reference: `non-linear-careers.md` - Comprehensive prompt reference covering all non-linear paths with assessment frameworks
- New reference: `non-linear-careers-template.md` - Structured output template for exploration results
- New reference: `alternative-career-paths-research.md` - Compiled research data on non-linear career paths, entrepreneurship, startups, public sector, charity, portfolio careers, career pivots, and intrapreneurship
- Non-linear career stage guidance in career-stage-context.md (Early Career through Late Career)
- Non-linear goal examples in three-month-plan.md (business validation, Civil Service applications, charity trustee positions, consulting launch, intrapreneurship, skill stacking)
- Non-linear Plan B options in three-month-plan-template.md
- New workflow pattern (Pattern D2: Non-Linear Career Exploration) in workflow-planner.md
- New power user scenarios: Non-Linear Career Pivot and Entrepreneurship Validation in power-user-strategies.md
- Non-Linear Career Exploration preparation checklist in preparation-checklist.md
- 8 new routing entries in help command for non-linear career queries
- 5 new routing entries in quick-start command for non-linear alternatives
- Non-linear career exploration output tracking in status command
- Career Transitions examples (non-linear exploration, public sector transition) in full-overview.md

### Changed
- Career Transitions skill expanded from 2 to 3 capabilities
- Career Transitions description updated with non-linear career triggers and tags (entrepreneurship, startup, founder, business, public-sector, charity, non-profit, non-linear, intrapreneurship, career-pivot)
- Career Transitions quick-start examples expanded with 8 new example prompts
- Career Navigator three-month-plan.md updated with guidance to consider non-linear options and proactively suggest /career-transitions when users seem stuck or questioning traditional employment
- Skill tips updated with Non-Linear Career Explorer tips, common mistakes, and iteration strategy
- Plugin version bumped to 1.7.0
- Updated all commands (help, quick-start, status) with non-linear career routing
- Updated all getting-started references (full-overview, skill-tips, workflow-planner, power-user-strategies, preparation-checklist, SKILL.md)
- README updated with non-linear career features, output files, and examples
- Marketplace description updated with non-linear career exploration

---

## [1.6.0] - 2026-03-03

### Added
- **New skill: `/ai-impact-assessment`** - AI impact analysis for career planning
  - Phase 1 research reference for understanding AI disruption across industries
  - Phase 2 assessment and action plan reference for personalised AI readiness
  - Output template for structured AI impact reports
- **New reference: "Getting the Best from Career Helper"** guide in getting-started skill
  - Comprehensive guide to maximising value from all 10 skills
  - Tips, workflows, and strategies for effective use
- AI Impact Assessment integrated into help, quick-start, overview, and plugin manifest routing

### Changed
- Plugin version bumped to 1.6.0 (10 skills)
- Updated all getting-started references with AI Impact Assessment integration

---

## [1.5.1] - 2026-02-28

### Added
- **Ageism in employment support** for Interview Master skill (post-interview coaching & all capabilities)
  - New reference: `ageism-in-employment.md` — comprehensive UK law (Equality Act 2010), Employment Tribunal process, burden of proof, time limits, compensation, whistleblowing routes, EHRC role, recent case law (2024-2025), and honest assessment of practical reality vs. letter of the law
  - New reference: `age-discrimination-strategies.md` — practical CV strategies to reduce age bias, interview tactics for "overqualified" concerns, digital presence optimisation, skills to update (with free/affordable UK training resources), age-friendly employers and job boards, networking strategies for older workers
  - New reference: `emotional-support-resilience.md` — psychological impact of age-related rejection, long-service identity crisis (20-30 years at one company), NHS and charity support services with helpline numbers, cognitive reframing techniques (3 C's Framework), daily routine templates, confidence rebuilding, crisis contacts, and when to seek professional help
- New ageism persona in Interview Master — triggered when user mentions age discrimination, being "too old", "overqualified" as age proxy, long-service redundancy, or age-related rejection patterns. Loads all three ageism references alongside standard capability references
- Ageism routing in help command (5 new routing entries)
- Ageism routing in quick-start command (new situation option + follow-up question + 3 routing entries)
- Quick start examples for ageism in Interview Master skill

### Changed
- Plugin version bumped to 1.5.1
- Interview Master skill description updated to include ageism and age discrimination triggers
- Interview Master tags updated to include ageism, age-discrimination, overqualified
- Interview Master career stage adaptation updated with ageism support references
- Updated all commands (help, quick-start) with ageism routing

---

## [1.5.0] - 2026-02-27

### Added
- **New skill: `/social-media-review`** - Lightweight social media check through a recruiter's eyes
  - 3 capabilities: Quick Social Scan, Platform Deep-Dive, Privacy & Cleanup Guide
  - Designed for graduates, early career, and anyone wanting a fast health check
  - GREEN/AMBER/RED flagging system with "3-second recruiter test"
  - Graduate-specific guidance that normalises having a social life
  - Quick wins list (5 things fixable in 10 minutes)
  - Platform-specific privacy settings walkthrough
  - Clear upgrade path to `/employer-footprint` for full scored dashboard
- Cross-linking between `/employer-footprint` and `/social-media-review` with comparison table
- Social Media Review tips in getting-started skill-tips reference
- Routing for `/social-media-review` in help, quick-start, and status commands
- Output file patterns `*-social-media-review.md` and `*-social-cleanup-guide.md` in status tracking

### Changed
- Plugin version bumped to 1.5.0 (9 skills)
- Updated all commands (help, quick-start, status) with social-media-review routing
- Updated getting-started references (full-overview, skill-tips, SKILL.md)
- Updated README with new skill in skills table, output files, and description

---

## [1.4.0] - 2026-02-27

### Added
- **New skill: `/employer-footprint`** - Digital footprint analysis through an employer's eyes
  - 4 capabilities: Full Footprint Analysis, Social Media Audit, Employer Impression Report, Interview Questions from Footprint
  - Agentic deep-research swarm architecture with 8 parallel research agents
  - Credit-report style dashboard with 8 scored dimensions (1-10 scale, traffic-light indicators)
  - Channels audited: Google, LinkedIn, Twitter/X, GitHub, Facebook, Instagram, Medium, YouTube, Stack Overflow, personal websites, news/media
  - CV-to-online-presence consistency checking
  - Company culture alignment mapping when target employer provided
  - Generates likely interview questions from publicly visible content
  - Recommends next career-helper skills based on findings
  - 5 reference files: digital-footprint-audit, footprint-dashboard-template, social-media-audit, employer-impression-analysis, interview-questions-from-footprint, deep-research-reflection
- Workspace persistence tip added across getting-started overview and README
- Footprint-first workflow pattern added to workflow-planner (Pattern A Step 0, Pattern C Step 0)
- Employer Footprint tips section added to skill-tips reference
- Footprint-First Approach added as Strategy 7 in power-user-strategies
- Digital footprint preparation checklist added to preparation-checklist reference
- Output file patterns for footprint dashboard, employer impression, social media audit, footprint interview questions in status tracking

### Changed
- Plugin version bumped to 1.4.0 (8 skills)
- Updated all commands (help, quick-start, status) with employer-footprint routing
- Updated all getting-started references with new skill examples and integration
- Updated skills workflow diagram to show footprint audit as entry point
- Renumbered power-user strategies (Output Maintenance became Strategy 8)

---

## [1.3.0] - 2026-02-14

### Added
- **New skill: `/ned-ai-helper`** - AI governance for Non-Executive Directors, Board Governors, and Charity Trustees
  - 5 capabilities: Challenge an AI Proposal, Risk Assessment, Governance Structure Design, Change Readiness Assessment, Human-in-the-Loop Assessment
  - 14 persona templates covering different board and trustee roles
  - Deep research methodology for AI governance topics
  - UK regulatory focus (AI Safety Institute, ICO, FCA) with international awareness
- Getting-started skill with 5 capabilities: Full Overview, Preparation Checklist, Workflow Planner, Skill-by-Skill Tips, Power User Strategies
  - Career-level awareness across all stages (graduate to late career)
  - 6 workflow patterns for different situations
  - 7 power user strategies

### Changed
- Plugin version bumped to 1.3.0 (7 skills)
- All skill names renamed to UK spelling (optimiser, not optimizer)
- Updated all commands and routing for new skills

---

## [1.2.0] - 2026-01-20

### Changed
- Updated install instructions for Claude co-worker format
- Plugin version bumped to 1.2.0

---

## [1.1.0] - 2025-12-15

### Added
- LinkedIn Coach: copy/paste and screenshot alternatives for profile access (LinkedIn blocks WebFetch)

### Fixed
- Replaced direct LinkedIn URL fetch requests with human-in-the-loop fallbacks

---

## [1.0.0] - 2025-12-01

### Added
- **Initial marketplace release** with 5 focused skills:
  - `/application-optimiser` - Company research, ATS CV rewriting, application strategy
  - `/linkedin-coach` - Profile audit, headline optimisation, content strategy, post review, video scripts
  - `/interview-master` - Interview prep, mock interviews, interviewer perspective reports, post-interview coaching
  - `/career-navigator` - Networking intelligence, 3-month plans, salary negotiation, offer evaluation
  - `/career-transitions` - Portfolio and fractional careers, AI readiness assessment
- 3 commands: `/career-helper:help`, `/career-helper:quick-start`, `/career-helper:status`
- Region-aware guidance (UK, US, EU, APAC)
- Career stage adaptation (graduate to late career)
- Deep research validation workflow
- Template-driven outputs with citation requirements

---

## Pre-1.0 History

| Version | Date | Summary |
|:--------|:-----|:--------|
| 0.4.0 | 2025-11 | LinkedIn headline optimisation |
| 0.3.0 | 2025-11 | Post-interview coaching capability |
| 0.2.0 | 2025-10 | Interviewer's perspective reports, deep research validation |
| 0.1.0 | 2025-10 | Initial commit - Career Helper skill |

---

*Career Helper Plugin | Prosper AI Consulting, UK*
