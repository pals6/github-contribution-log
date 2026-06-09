# Contribution 1: Add documentation for the `canvas_only` kwarg

**Contribution Number:** 1
**Student:** Pallavi Bichpuriya
**Issue:** [napari-animation #235: [Docs] Add documentation for the canvas_only kwarg](https://github.com/napari/napari-animation/issues/235)
**Status:** Phase IV — Pull Request Submitted / Awaiting Review

---

## Why I Chose This Issue

I chose this issue because it is a well-scoped documentation contribution in an open-source Python project. Since this is my first contribution for AI301, I wanted to start with an issue that was understandable, low-risk, and still connected to real project usability. The issue asks for documentation around the `canvas_only` keyword argument, which affects how users export animations from `napari-animation`.

This issue also matches my learning goals for the course because it required me to read an unfamiliar repository, trace how a parameter is used across the API and GUI, and document the behavior clearly for future users. Even though it is a documentation issue, it still involved codebase exploration and verification against the actual implementation, which is an important open-source contribution skill.

---

## Understanding the Issue

### Problem Description

The project had a `canvas_only` keyword argument, but its behavior was not clearly documented for users. The issue requested explicit documentation explaining how `canvas_only` works both in the GUI Save dialog and in programmatic usage.

### Expected Behavior

Users should be able to understand:

* what `canvas_only=True` does
* what `canvas_only=False` does
* how the option appears in the GUI Save dialog
* how to use the option programmatically with `animation.animate(...)`

### Current Behavior

Before this contribution, the README included a scripting example using `canvas_only=False`, but it did not explain what the argument meant or when a user should change it. This could make the option confusing for users who are exporting animations and trying to decide whether to include only the napari canvas or the full viewer interface.

### Affected Components

The main components involved were:

* `README.md` — main documentation file updated in this contribution
* `docs/index.md` — includes the README in the rendered documentation
* `napari_animation/animation.py` — defines the `animate()` API and `canvas_only` parameter
* `napari_animation/_qt/savedialog_widget.py` — contains the GUI Save dialog checkbox for “Canvas only”
* `napari_animation/viewer_state.py` — helped confirm how canvas-only rendering is handled

---

## Reproduction Process

### Environment Setup

I forked and cloned the `napari-animation` repository locally from GitHub. Since this was a documentation issue, the main setup required was repository navigation, searching the codebase, and reviewing how the docs are structured.

Repository fork: [pals6/napari-animation](https://github.com/pals6/napari-animation)

### Steps to Reproduce

1. Open the existing `README.md`.
2. Review the scripting section that shows `animation.animate('demo.mov', canvas_only=False)`.
3. Search the codebase for `canvas_only`.
4. Observe that the option exists in the API and GUI, but the README does not clearly explain it.

### Reproduction Evidence

* **Commit showing reproduction:** [Add commit link here]
* **Screenshots/logs:** Not applicable for this documentation issue.
* **My findings:** The README used `canvas_only` in an example, but did not explain what the parameter does. I also found that `docs/index.md` includes the README, so updating the README would update the rendered documentation page as well.

---

## Solution Approach

### Analysis

The root issue was a documentation gap rather than a code defect. The `canvas_only` behavior already existed in the project, but users did not have a clear explanation of the option in the main docs. I reviewed the relevant source files to avoid inventing behavior and to make sure the documentation matched the implementation.

During review, I also found that a possible note about `scale_factor` would have repeated a claim from the docstring that did not match the actual implementation. I removed that note and kept this PR focused only on accurately documenting `canvas_only`.

### Proposed Solution

Add a small **Canvas only** subsection to `README.md` after the scripting example. The new section explains:

* that both the GUI and programmatic API support the `canvas_only` option
* that `canvas_only=True` exports only the napari canvas / layer visualization area
* that `canvas_only=False` includes the full napari viewer / interface context
* that the GUI Save dialog has a **Canvas only** checkbox
* how to call `animation.animate(..., canvas_only=True)` programmatically

### Implementation Plan

Using UMPIRE framework:

**Understand:**
The issue asks for explicit documentation of the `canvas_only` keyword argument for both GUI and programmatic usage.

**Match:**
I searched the repository for existing usage of `canvas_only` and reviewed the README style. The README already uses MyST-style Markdown and includes scripting examples, so adding a short subsection there matched the existing documentation pattern.

**Plan:**

1. Search for `canvas_only` across the repository.
2. Review the API docstring in `animation.py`.
3. Review the GUI Save dialog implementation in `savedialog_widget.py`.
4. Confirm that `docs/index.md` includes the README.
5. Add a focused README subsection explaining the option.
6. Review the final diff to ensure the PR is docs-only.

**Implement:**
Branch: `docs/canvas-only-kwarg`
Pull Request: [Add PR link here]

**Review:**
Self-review checklist:

* [x] Change is limited to documentation
* [x] README wording matches existing code behavior
* [x] No unrelated cleanup changes included
* [x] Programmatic example is included
* [x] GUI Save dialog behavior is mentioned
* [x] The PR references and closes the original issue

**Evaluate:**
I verified the change by reviewing the final diff, confirming only `README.md` was changed, and checking that the added documentation matched the source behavior.

---

## Testing Strategy

### Unit Tests

Not applicable because this is a documentation-only change.

### Integration Tests

Not applicable because no functionality was changed.

### Manual Testing

Manual verification completed:

* [x] Searched the codebase for `canvas_only`
* [x] Reviewed `animation.py` for the API parameter
* [x] Reviewed `savedialog_widget.py` for the GUI checkbox behavior
* [x] Confirmed `docs/index.md` includes `README.md`
* [x] Reviewed the final README diff before committing
* [x] Confirmed the change is documentation-only

---

## Implementation Notes

### Week 1 Progress

This week, I selected my first open-source issue for AI301 and chose napari-animation issue #235. I reviewed the issue description, forked and cloned the repository, searched the codebase for `canvas_only`, and identified the correct documentation location.

I made a focused documentation update in `README.md` explaining the `canvas_only` keyword argument for both GUI and programmatic usage. I also used AI tools to help inspect the repository and review the documentation wording, but I manually verified the final behavior against the code before committing.

### Code Changes

* **Files modified:** `README.md`
* **Key commits:** [Add commit link here]
* **Approach decisions:** I kept the PR documentation-only and avoided changing source code or unrelated docstring wording. I also removed a proposed `scale_factor` note because the implementation did not clearly support that claim.

---

## Pull Request

**PR Link:** [Add PR URL here]

**PR Description:**

Adds documentation for the `canvas_only` keyword argument, requested in issue #235.

The new README section explains:

* what `canvas_only=True` does
* what `canvas_only=False` does
* how the option maps to the GUI Save dialog
* how to use the option programmatically with `animation.animate(...)`

**Maintainer Feedback:**

* No maintainer feedback received yet.

**Status:** Awaiting review.

---

## Learnings & Reflections

### Technical Skills Gained

I learned how to navigate an unfamiliar open-source Python repository, search for a parameter across API and GUI code, and verify documentation wording against the actual implementation. I also learned how documentation issues can still require careful code reading to avoid inaccurate explanations.

### Challenges Overcome

One challenge was making sure the documentation did not overclaim behavior. During review, I found that a possible note about `scale_factor` repeated a docstring claim that did not match the implementation. I decided not to include that note, which helped keep the PR accurate and focused.

### What I'd Do Differently Next Time

Next time, I would check the implementation before drafting any explanatory notes, especially when documentation and code behavior may not fully match. I would also look earlier for how the docs are rendered so I can confirm the best file to update before editing.

---

## Resources Used

* [napari-animation issue #235](https://github.com/napari/napari-animation/issues/235)
* [napari-animation repository](https://github.com/napari/napari-animation)
* [My fork: pals6/napari-animation](https://github.com/pals6/napari-animation)
* `README.md`
* `docs/index.md`
* `napari_animation/animation.py`
* `napari_animation/_qt/savedialog_widget.py`
* `napari_animation/viewer_state.py`

---

## AI Usage Log

### Tools Used

* Codex
* Claude Code
* ChatGPT

### How AI Helped

Codex helped inspect the repository and identify where `canvas_only` appeared in the codebase and documentation. Claude Code reviewed the documentation diff and caught that a proposed `scale_factor` note was not fully supported by the implementation. ChatGPT helped plan the open-source workflow, draft the issue comment, review next steps, and structure this contribution log.

### How I Verified AI Output

I manually reviewed the relevant files, checked the final diff, confirmed that only documentation was changed, and removed wording that was not supported by the implementation.

### Reflection

AI helped speed up repository exploration and documentation drafting, but I remained responsible for the final content. The most important part of the process was verifying AI suggestions against the actual code before submitting the PR.
