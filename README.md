# Contribution 1: Add documentation for the `canvas_only` kwarg

**Contribution Number:** 1
**Student:** Pallavi Bichpuriya
**Issue:** [napari-animation #235: Add documentation for the `canvas_only` kwarg](https://github.com/napari/napari-animation/issues/235)
**Status:** Phase IV — Pull Request Submitted / Awaiting Review

---

## Why I Chose This Issue

I chose this issue because it is a well-scoped documentation contribution in an open-source Python project. Since this is my first contribution for AI301, I wanted to begin with an issue that was understandable, low-risk, and connected to real project usability. The issue asks for clearer documentation around the `canvas_only` keyword argument, which affects how users export animations from `napari-animation`.

This issue also matches my learning goals because it required me to read an unfamiliar repository, trace how a parameter is used across the programmatic API and GUI, and document the behavior clearly for future users. Even though this is a documentation issue, it still involved codebase exploration, implementation tracing, source verification, Git workflow, and pull request preparation.

---

## Understanding the Issue

### Problem Description

The project already had a `canvas_only` keyword argument, but its behavior was not clearly explained in the main documentation. The existing README used the argument in a scripting example without explaining what it controls.

The issue requested explicit documentation covering both:

* how `canvas_only` works in the GUI Save dialog
* how to use it programmatically with `animation.animate(...)`

### Expected Behavior

Users should be able to understand:

* what `canvas_only=True` does
* what `canvas_only=False` does
* that `canvas_only=True` is the default
* how the option appears in the GUI Save dialog
* how to pass the option programmatically to `animation.animate(...)`

### Current Behavior

Before this contribution, the README included the following scripting example:

```python
animation.animate('demo.mov', canvas_only=False)
```

However, the README did not explain what `canvas_only` meant, what its default value was, or when a user should choose `True` instead of `False`.

A user would need to inspect the source code to understand whether an exported animation includes only the napari canvas or the complete viewer interface.

### Affected Components

The main components involved were:

* `README.md` — the main documentation file updated in this contribution
* `docs/index.md` — includes the README in the rendered documentation
* `napari_animation/animation.py` — defines the `animate()` API and `canvas_only` parameter
* `napari_animation/_qt/savedialog_widget.py` — contains the GUI Save dialog and **Canvas only** checkbox
* `napari_animation/viewer_state.py` — contains canvas and viewer rendering behavior
* `napari_animation/frame_sequence.py` — helped verify how exported frames are rendered

---

## Reproduction Process

### Environment Setup

I forked and cloned the `napari-animation` repository locally on macOS.

* **Fork:** [pals6/napari-animation](https://github.com/pals6/napari-animation)
* **Working branch:** [docs/canvas-only-kwarg](https://github.com/pals6/napari-animation/tree/docs/canvas-only-kwarg)

Because this was a documentation issue rather than an application defect, reproducing it did not require running the complete napari GUI. I reproduced the issue by inspecting the existing documentation and tracing the documented parameter through the source code.

I searched the repository for all references to `canvas_only` and reviewed the following files:

* `README.md`
* `docs/index.md`
* `napari_animation/animation.py`
* `napari_animation/_qt/savedialog_widget.py`
* `napari_animation/viewer_state.py`
* `napari_animation/frame_sequence.py`

No major environment setup blockers were encountered.

### Steps to Reproduce

1. Open `README.md` in the repository.

2. Navigate to the **Scripting** section.

3. Locate the existing example:

   ```python
   animation.animate('demo.mov', canvas_only=False)
   ```

4. Search the README for an explanation of `canvas_only`.

5. Observe that the argument is used, but its purpose, default value, and possible behaviors are not explained.

6. Search the source code for `canvas_only`.

7. Open `napari_animation/animation.py` and confirm that `animate()` defines `canvas_only=True` by default.

8. Open `napari_animation/_qt/savedialog_widget.py` and confirm that the GUI exposes the same setting through the **Canvas only** checkbox.

9. Confirm that the GUI checkbox is enabled by default.

10. Open `docs/index.md` and confirm that it includes `README.md`, making the README the appropriate documentation location.

11. Return to the README and confirm that users still have no explicit explanation of the option.

### Expected Result

The documentation should explain:

* how `canvas_only=True` affects exported animations
* how `canvas_only=False` affects exported animations
* how the option relates to the GUI Save dialog
* how to use the option programmatically

### Actual Result

The README uses `canvas_only=False` in a scripting example but does not explain what the argument controls.

### Reproduction Evidence

* **Working branch:** [docs/canvas-only-kwarg](https://github.com/pals6/napari-animation/tree/docs/canvas-only-kwarg)
* **Issue:** [napari-animation #235](https://github.com/napari/napari-animation/issues/235)
* **Implementation commit:** [ADD YOUR COMMIT URL HERE]
* **Screenshots/logs:** Not applicable for this documentation issue.
* **My findings:** The `canvas_only` option already existed in both the programmatic API and the GUI Save dialog, but the README did not explain what it controls. I also confirmed that `docs/index.md` includes the README, so updating `README.md` updates the rendered documentation page.

---

## Solution Approach

### Analysis

The root issue was a documentation gap rather than a functional defect. The `canvas_only` option already existed and worked through both the programmatic API and the GUI Save dialog, but users did not have a clear explanation of its behavior in the main documentation.

The README’s **Scripting** section already used `canvas_only=False`, making that section the most natural location for the explanation.

During my review, I also found a separate inconsistency related to `scale_factor`. The `animate()` docstring suggested that `scale_factor` only applied when `canvas_only=True`, but the implementation in `frame_sequence.py` appeared to apply it regardless of the `canvas_only` value. To avoid repeating a claim that was not supported by the implementation, I removed the proposed `scale_factor` note and kept this contribution focused on issue #235.

### Proposed Solution

Add a small **Canvas only** subsection to `README.md` immediately after the existing scripting example.

The new section should explain:

* that the GUI and programmatic API both support the `canvas_only` option
* that `canvas_only=True` exports only the napari canvas or layer visualization area
* that `canvas_only=False` includes the full napari viewer interface
* that the GUI Save dialog exposes the option through the **Canvas only** checkbox
* that the checkbox is enabled by default
* how to use `canvas_only` programmatically with `animation.animate(...)`

### Implementation Plan

Using the adapted UMPIRE framework:

#### Understand

The `canvas_only` argument is available to users, but its purpose is not explicitly documented. Users should not have to inspect the source code to determine what `True` and `False` mean.

#### Match

I searched the repository for existing uses of `canvas_only` and reviewed the existing documentation style.

The README already:

* contains the main scripting example
* uses sentence-case headings
* uses fenced Python examples
* is included in the documentation site through `docs/index.md`

Adding a short subsection after the scripting example therefore matches the project’s existing documentation structure.

#### Plan

1. Search for `canvas_only` across the repository.
2. Review the `animate()` API definition in `animation.py`.
3. Review the GUI Save dialog implementation in `savedialog_widget.py`.
4. Review canvas and full-viewer rendering behavior.
5. Confirm that `docs/index.md` includes `README.md`.
6. Add a focused **Canvas only** subsection after the scripting example.
7. Explain the difference between `canvas_only=True` and `canvas_only=False`.
8. Mention the matching GUI Save dialog checkbox.
9. Add a short programmatic example.
10. Keep the change limited to `README.md`.
11. Review the final diff to ensure no unrelated changes are included.

#### Implement

* **Working branch:** [docs/canvas-only-kwarg](https://github.com/pals6/napari-animation/tree/docs/canvas-only-kwarg)
* **Implementation commit:** [ADD YOUR COMMIT URL HERE]
* **Pull request:** [ADD YOUR PR URL HERE]

#### Review

Self-review checklist:

* [x] The change is limited to documentation.
* [x] Only `README.md` was modified.
* [x] The documentation wording matches the implementation.
* [x] No unrelated cleanup changes were included.
* [x] The programmatic example is included.
* [x] The GUI Save dialog behavior is mentioned.
* [x] The default value is documented.
* [x] The formatting matches the existing README style.
* [x] The PR references and closes the original issue.

#### Evaluate

I planned to verify the contribution by:

* searching the updated README for `canvas_only`
* reviewing the rendered Markdown structure
* confirming the new section covers GUI and programmatic usage
* reviewing the final Git diff
* confirming that only `README.md` changed
* checking the pull request’s automated CI results

---

## Testing Strategy

### Unit Tests

Not applicable because this is a documentation-only change and no application behavior was modified.

### Integration Tests

Not applicable because no production logic or integration behavior was changed.

### Manual Testing

Manual verification completed:

* [x] Searched the codebase for `canvas_only`.
* [x] Reviewed `animation.py` for the API parameter and default value.
* [x] Reviewed `savedialog_widget.py` for the GUI checkbox behavior.
* [x] Reviewed rendering-related source code.
* [x] Confirmed `docs/index.md` includes `README.md`.
* [x] Reviewed the final README diff before committing.
* [x] Confirmed only `README.md` was changed.
* [x] Removed wording that was not supported by the implementation.
* [x] Confirmed the documentation contains a programmatic example.
* [x] Confirmed the documentation explains both `True` and `False` behavior.

---

## Implementation Notes

### Phase II: Reproduce and Plan

For Phase II, I confirmed that this issue was a documentation gap rather than a functional defect. I reproduced the problem by locating the existing `canvas_only=False` scripting example in the README and confirming that no explanation of the argument was provided.

I then traced the option through the API and GUI code to understand its behavior. I identified `README.md` as the correct file to update because `docs/index.md` includes it in the rendered documentation.

Before implementing the change, I planned to:

1. Add a focused **Canvas only** subsection after the scripting example.
2. Explain the behavior of `canvas_only=True`.
3. Explain the behavior of `canvas_only=False`.
4. Connect the programmatic option to the GUI **Canvas only** checkbox.
5. Include a short programmatic example.
6. Keep the change limited to documentation.
7. Verify the wording against the implementation.
8. Review the final diff before committing.

**Phase II status:** Complete.

### Week 1 Progress

This week, I selected my first open-source issue for AI301 and chose napari-animation issue #235.

I:

* reviewed the issue description
* forked and cloned the repository
* created and pushed a working branch
* searched the codebase for `canvas_only`
* reviewed the relevant API and GUI source files
* identified the correct documentation location
* wrote a solution plan
* added the documentation update
* manually reviewed the final diff
* committed and pushed the change
* opened a pull request to the upstream repository

I used AI tools to assist with repository navigation and review, but I manually verified the final behavior against the code before submitting the contribution.

### Code Changes

* **Files modified:** `README.md`
* **Working branch:** [docs/canvas-only-kwarg](https://github.com/pals6/napari-animation/tree/docs/canvas-only-kwarg)
* **Approach decisions:** I kept the PR documentation-only and avoided changing source code or unrelated docstring wording. I also removed a proposed `scale_factor` note because the implementation did not clearly support that claim.

---

## Pull Request

**PR Link:** (https://github.com/napari/napari-animation/pull/274)

### PR Description

Adds documentation for the `canvas_only` keyword argument requested in issue #235.

The new README section explains:

* what `canvas_only=True` does
* what `canvas_only=False` does
* that `canvas_only=True` is the default
* how the option maps to the GUI Save dialog
* how to use the option programmatically with `animation.animate(...)`

The change is documentation-only and is added to the README, which is included in the rendered documentation through `docs/index.md`.

### Maintainer Feedback

* No maintainer feedback received yet.

### Pull Request Status

Awaiting maintainer review.

---

## Learnings & Reflections

### Technical Skills Gained

I learned how to:

* navigate an unfamiliar open-source Python repository
* search for a parameter across API, GUI, and rendering code
* verify documentation wording against actual implementation behavior
* identify how a project’s documentation pages are assembled
* create a focused Git branch and commit
* submit a pull request to an upstream repository
* keep a contribution narrowly scoped to the original issue

I also learned that documentation issues can still require careful code reading. Even when no functionality is changed, inaccurate documentation can mislead users, so each statement must be checked against the implementation.

### Challenges Overcome

The main challenge was ensuring that the documentation did not overclaim behavior.

During review, I found that a possible note about `scale_factor` repeated a statement from a docstring that did not appear to match the implementation in `frame_sequence.py`. Instead of including uncertain information, I removed the note and kept the contribution focused on behavior that I could verify.

Another challenge was determining the correct documentation location. I confirmed that `docs/index.md` includes `README.md`, so a README update was sufficient to expose the new section in the rendered documentation.

### What I’d Do Differently Next Time

Next time, I would inspect the implementation before drafting explanatory documentation, especially when existing docstrings may not fully match the code.

I would also identify how the project builds its documentation earlier in the process so I can confirm the correct file before beginning an edit.

For a future contribution, I would try to document the reproduction and solution plan before starting implementation rather than reconstructing some of those steps after the PR was already submitted.

---

## Resources Used

* [napari-animation issue #235](https://github.com/napari/napari-animation/issues/235)
* [napari-animation upstream repository](https://github.com/napari/napari-animation)
* [My fork: pals6/napari-animation](https://github.com/pals6/napari-animation)
* [Working branch: docs/canvas-only-kwarg](https://github.com/pals6/napari-animation/tree/docs/canvas-only-kwarg)
* `README.md`
* `docs/index.md`
* `napari_animation/animation.py`
* `napari_animation/_qt/savedialog_widget.py`
* `napari_animation/viewer_state.py`
* `napari_animation/frame_sequence.py`

---

## AI Usage Log

### Tools Used

* Codex
* Claude Code
* ChatGPT

### How AI Helped

Codex helped inspect the repository and identify where `canvas_only` appeared in the codebase and documentation.

Claude Code reviewed the documentation diff against the implementation and identified that a proposed `scale_factor` note repeated a docstring claim that did not appear to match the actual code.

ChatGPT helped:

* evaluate the issue as a first open-source contribution
* plan the contribution workflow
* draft the initial issue comment
* prepare repository investigation prompts
* structure the Phase II reproduction and solution plan
* prepare the pull request description
* organize this contribution log

### How I Verified AI Output

I manually reviewed:

* the relevant source files
* the existing README
* the documentation structure
* the final Git diff
* the list of modified files
* the wording describing `canvas_only=True` and `canvas_only=False`

I confirmed that only documentation was changed and removed wording that was not supported by the implementation.

### Reflection

AI helped reduce the time required to navigate an unfamiliar repository and review the documentation. However, I remained responsible for every claim included in the contribution.

The most important part of the process was checking AI-generated suggestions against the source code before submitting the pull request.
