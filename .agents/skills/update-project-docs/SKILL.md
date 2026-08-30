---
name: update-project-docs
description: >-
  Keep GEMINI.md (Engineering Analysis & Architecture) and README.md (User-facing feature summary & run guide)
  updated and synchronized whenever code changes, bug fixes, refactoring, or new features are introduced in the project.
---

# Documentation Synchronization Skill

This skill defines the standard procedure for keeping the project's documentation—specifically [`GEMINI.md`](file:///d:/Playground/ParbonStatic/Janmashtami2026/GEMINI.md) and [`README.md`](file:///d:/Playground/ParbonStatic/Janmashtami2026/README.md)—strictly synchronized with the codebase whenever modifications are made to [`index.html`](file:///d:/Playground/ParbonStatic/Janmashtami2026/index.html) or other project assets.

---

## 1. Documentation Roles & Division of Responsibilities

| Documentation File | Target Audience & Scope | Key Sections to Maintain |
| :--- | :--- | :--- |
| **[`GEMINI.md`](file:///d:/Playground/ParbonStatic/Janmashtami2026/GEMINI.md)** | **Engineering Analysis & Architectural Spec**<br>Deep technical documentation, commit history, architectural diagrams, mathematical formulations, Web Audio DSP pipelines, canvas rendering internals, and performance metrics. | • Project Overview & Design Tokens<br>• Chronological Commit History & Git Graph<br>• Subsystem Architecture Diagrams (ASCII / Mermaid)<br>• Mathematical/Physical Kinematic Equations<br>• Procedural Audio Synthesis Parameters<br>• Performance & Quality Metrics Table<br>• Engineering Summary |
| **[`README.md`](file:///d:/Playground/ParbonStatic/Janmashtami2026/README.md)** | **User & Developer Overview**<br>High-level festival introduction, key interactive feature highlights, running instructions, local server commands, technology stack, and links to engineering deep-dives. | • Overview of `index.html`<br>• Key Features & Interactive Modules list<br>• Running / Local Hosting Instructions<br>• Technology Stack details<br>• Reference link to `GEMINI.md` |

---

## 2. When to Execute This Skill

Execute this workflow **every time**:
1. A new feature, interactive module, or visual component is added.
2. An existing feature or physics/audio algorithm is modified, refined, or optimized.
3. CSS styles, color tokens, animations, or layout structures are updated.
4. Performance optimizations (e.g., canvas rendering, DOM throttling, paint reduction) are implemented.
5. A git commit is created or prepared for staging.

---

## 3. Step-by-Step Execution Workflow

### Step 1: Analyze the Delta (Code Changes)
1. Inspect the modified files using `git status`, `git diff`, or file review tools.
2. Categorize the changes into relevant engineering domains:
   - **DOM / Semantic Structure**: New sections, accessibility tags, dialogs, forms.
   - **CSS / Visual Design**: New CSS variables, animations, 3D perspective rules, responsive breakpoints.
   - **Interactive Physics / Math**: Pendulum mechanics, collision, gravity, particle dynamics.
   - **Procedural Audio (Web Audio API)**: Oscillator types, frequency sweeps, envelope timings, gain ramps.
   - **Canvas Rendering / Blitting**: Offscreen caching, particle loops, frame throttling.
   - **Performance**: Event listeners (`requestAnimationFrame`, passive flags), GPU layer promotion, backdrop filter replacements.

### Step 2: Update [`GEMINI.md`](file:///d:/Playground/ParbonStatic/Janmashtami2026/GEMINI.md)
1. **Commit History / Change Log**:
   - If a new commit was made, append a new commit analysis block with the commit hash, author, date, lines changed, and detailed breakdown of features/optimizations.
   - Update the `mermaid` `gitGraph` to reflect the branch / commit topology.
2. **Subsystem Architecture**:
   - Update the ASCII / Mermaid subsystem architecture block to include new modules or data flows.
3. **Deep-Dive Technical Analysis**:
   - If new physics or math was added, include the exact mathematical formulas (e.g., LaTeX formulas `$$\theta(t) = ...$$`) and code snippets.
   - If audio synthesis was altered, detail oscillator routing, frequency curves, and filter parameters.
   - If canvas particle rendering changed, detail sprite blitting dimensions and performance benchmarks.
4. **Performance Metrics Table**:
   - Update the performance table with any new architectural decisions and their corresponding frame-rate / memory benefits.

### Step 3: Update [`README.md`](file:///d:/Playground/ParbonStatic/Janmashtami2026/README.md)
1. **Feature Highlights**:
   - Add or update numbered feature items under "Key Features & Interactive Modules" with user-friendly descriptions and emoji badges.
2. **Usage / Running Guide**:
   - Ensure execution instructions remain accurate if new runtime requirements or server recommendations arise.
3. **Tech Stack**:
   - Update the technology breakdown if new Web APIs or external font families are used.

### Step 4: Verification & Consistency Check
1. **Markdown Formatting**: Validate that all code blocks have appropriate language tags (`html`, `css`, `javascript`, `bash`, `mermaid`, `markdown`).
2. **File Links**: Ensure all relative links use GitHub markdown format with valid `file:///` URIs.
3. **Cross-Reference Consistency**: Verify that terminology, CSS class names, and audio frequencies mentioned in `GEMINI.md` and `README.md` exactly match [`index.html`](file:///d:/Playground/ParbonStatic/Janmashtami2026/index.html).
