# CIS53 Content Repository — Feature Summary (Concise)

## 🔹 Core Overview
A Git-based content repository for **CIS 53 (Introduction to Intrusion Detection)** that organizes **labs, quizzes, final exam, and lecture notes**. Designed for ingestion by **Cyber Grader** through automated sync workflows. Content is stored as Markdown/YAML assets with validation metadata and version tracking.

---

## 🚀 Key Features

### 1. **Repository Architecture**
- **Directory Structure:** `labs/`, `quizzes/`, `final/`, `notes/`, `shared/` (common assets, media, rubrics).
- **Content Format:** Markdown for narrative instructions, YAML/JSON for structured assessment data.
- **Automation Ready:** Consistent schema enables Cyber Grader pull-and-parse pipelines.
- **Version Control:** Git commits provide history, tagging for course releases (`v{term}-{release}`).

---

### 2. **Metadata & Manifest**
- Root-level `course.yaml` defines course term, pacing, grading weights, and sync settings.
- Each assessment folder includes an `index.yaml` manifest describing modules, prerequisites, and grading rules.
- Optional `assets/` subdirectories provide supporting files with checksum tracking.

---

### 3. **Labs**
- Located under `labs/{module}/` with:
  - `README.md` (student instructions) featuring objectives, prerequisites, and submission guidance.
  - `flags.yaml` defining validation (`exact`, `regex`, `script`, `file_hash`).
  - `rubric.yaml` capturing scoring breakdown and partial credit rules.
- Supports multiple lab variants via `variants/` subfolders that inherit base metadata.
- Change log maintained via `CHANGELOG.md` per lab to surface updates for Cyber Grader release notes.

---

### 4. **Quizzes**
- Stored in `quizzes/{module}/quiz.yaml`.
- YAML schema captures question banks (MCQ, true/false, short answer, scenario), randomization rules, and per-question scoring.
- Includes `feedback.md` for post-quiz explanations and `settings.yaml` for attempt limits and availability windows.
- Version tags aligned with Git commits ensure deterministic grading.

---

### 5. **Final Exam**
- Organized in `final/{stage}/` directories to support multi-stage structure.
- Each stage contains:
  - `exam.yaml` combining objective items (auto-graded) and subjective prompts (rubric references).
  - `timeline.yaml` for availability windows, time limits, and unlock conditions.
  - `attachments/` for packet captures, logs, or evidence files.
- Aggregation rules defined in `final/summary.yaml` mapping stage scores to final grade weight.

---

### 6. **Lecture Notes & Media**
- Markdown-based lecture notes inside `notes/week-XX/README.md` with embedded resource links.
- `notes/media/` stores supplementary images, diagrams, and slide decks (preferably PDF/PNG).
- Optional `notes/index.yaml` lists modules, objectives, and related lab/quiz references for Cyber Grader dashboards.

---

### 7. **Validation & Tooling**
- `scripts/validate.py` runs schema and link checks prior to sync; recommended as a pre-commit hook and CI step.
- `schemas/` directory defines JSON Schema files for labs, quizzes, exam YAML validation.
- GitHub Actions workflow (`.github/workflows/ci.yml`) executes validation, lints Markdown, and publishes release artifacts.

---

### 8. **Cyber Grader Integration**
- `sync-config.yaml` specifies target Cyber Grader instance, API endpoints, and content mappings.
- Webhook-friendly structure so Cyber Grader can pull latest commit SHA, compare manifests, and ingest updates.
- Exports summary data (`exports/`) for debugging: manifest snapshots, schema validation reports, and changelog digests.

---

### 9. **Documentation & Onboarding**
- `CONTRIBUTING.md` outlines naming conventions, schema expectations, and review checklist.
- `STYLE.md` provides Markdown/YAML style guides, glossary, and taxonomy for intrusion detection topics.
- `ROADMAP.md` tracks planned content expansions (new labs, updated quizzes, supplemental resources).

---

### 10. **Quality Assurance**
- Each content area maintains unit-like tests via `tests/` referencing schema validators.
- Scheduled CI job performs nightly validation against Cyber Grader staging environment.
- Audit trail of changes captured through conventional commit messages and GitHub releases.

