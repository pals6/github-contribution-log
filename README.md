# Contribution 1: Add documentation for the `canvas_only` kwarg

**Contribution Number:** 1
**Student:** Pallavi Bichpuriya
**Issue:** [napari-animation #235: Add documentation for the `canvas_only` kwarg](https://github.com/napari/napari-animation/issues/235)
**Status:** Phase IV — Maintainer Feedback Addressed / Awaiting Follow-Up Review

---

## Why I Chose This Issue

I chose this issue because it is a well-scoped documentation contribution in an open-source Python project. Since this is my first contribution for AI301, I wanted to begin with an issue that was understandable, low-risk, and connected to real project usability. The issue asks for clearer documentation around the `canvas_only` keyword argument, which affects how users export animations from `napari-animation`.

This issue also matches my learning goals because it required me to read an unfamiliar repository, trace how a parameter is used across the programmatic API and GUI, and document the behavior clearly for future users. Even though this is a documentation issue, it still involved codebase exploration, implementation tracing, source verification, Git workflow, pull request preparation, and responding to maintainer feedback.

---

## Understanding the Issue

### Problem Description

The project already had a `canvas_only` keyword argument, but its behavior was not clearly explained in the main documentation. The existing README used the argument in a scripting example without explaining what it controls.

The issue requested explicit documentation covering:

* how `canvas_only` works in the GUI Save dialog
* how to use it programmatically with `animation.animate(...)`

### Expected Behavior

Users should be able to understand:

* what `canvas_only=True` does
* what `canvas_only=False` does
* that `canvas_only=True` is the default
* how the option appears in the GUI Save dialog
* how the option is passed programmatically to `animation.animate(...)`

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

I searched the repository for all references to `canvas_only` and reviewed:

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
* **Initial implementation commit:** [ADD INITIAL COMMIT URL HERE]
* **Maintainer-feedback revision commit:** [ADD REVISION COMMIT URL HERE]
* **Screenshots/logs:** Not applicable for this documentation issue.
* **My findings:** The `canvas_only` option already existed in both the programmatic API and the GUI Save dialog, but the README did not explain what it controls. I also confirmed that `docs/index.md` includes the README, so updating `README.md` updates the rendered documentation page.

---

## Solution Approach

### Analysis

The root issue was a documentation gap rather than a functional defect. The `canvas_only` option already existed and worked through both the programmatic API and GUI Save dialog, but users did not have a clear explanation of its behavior in the main documentation.

The README’s existing **Scripting** section already used `canvas_only=False`, making that example the most natural place to document the option.

During my investigation, I also found a separate inconsistency related to `scale_factor`. The `animate()` docstring suggested that `scale_factor` only applied when `canvas_only=True`, but the implementation in `frame_sequence.py` appeared to apply it regardless of the `canvas_only` value. To avoid repeating a claim that was not supported by the implementation, I excluded the `scale_factor` statement and kept this contribution focused on issue #235.

### Initial Proposed Solution

My initial approach was to add a separate **Canvas only** subsection after the scripting example. The section explained:

* the difference between `canvas_only=True` and `canvas_only=False`
* the default value
* the matching GUI Save dialog checkbox
* a separate programmatic example

After reviewing the pull request, the maintainer explained that this version overexplained information that could be incorporated into the existing scripting example.

### Revised Solution

Based on the maintainer’s feedback, I removed the separate subsection and duplicate programmatic example.

The final approach keeps the existing:

```python
animation.animate('demo.mov', canvas_only=False)
```

example and adds a concise explanation immediately below it:

```markdown
Set `canvas_only=True` to export only the napari canvas, or `False` to include the
full viewer interface. In the GUI Save dialog this corresponds to the **Canvas only**
checkbox, which is enabled by default.
```

This version documents the required behavior while matching the project’s preference for concise documentation.

### Implementation Plan

Using the adapted UMPIRE framework:

#### Understand

The `canvas_only` argument is available to users, but its purpose is not explicitly documented. Users should not have to inspect the source code to determine what `True` and `False` mean.

#### Match

I searched the repository for existing uses of `canvas_only` and reviewed the existing documentation style.

The README already:

* contains the main scripting example
* uses concise explanatory prose
* uses fenced Python examples
* is included in the documentation site through `docs/index.md`

The maintainer’s review clarified that the explanation should be integrated into the existing example rather than introduced as a separate section.

#### Plan

1. Search for `canvas_only` across the repository.
2. Review the `animate()` API definition in `animation.py`.
3. Review the GUI Save dialog implementation in `savedialog_widget.py`.
4. Review canvas and full-viewer rendering behavior.
5. Confirm that `docs/index.md` includes `README.md`.
6. Use the existing `animation.animate(..., canvas_only=False)` example as the programmatic demonstration.
7. Add a concise explanation immediately below the example.
8. Explain the difference between `canvas_only=True` and `canvas_only=False`.
9. Mention the equivalent **Canvas only** checkbox in the GUI Save dialog.
10. Keep the change limited to `README.md`.
11. Review the final diff to ensure no unrelated changes are included.
12. Respond to maintainer feedback and push the revision to the existing pull request.

#### Implement

* **Working branch:** [docs/canvas-only-kwarg](https://github.com/pals6/napari-animation/tree/docs/canvas-only-kwarg)
* **Initial implementation commit:** [ADD INITIAL COMMIT URL HERE]
* **Maintainer-feedback revision commit:** [ADD REVISION COMMIT URL HERE]
* **Pull request:** [napari-animation PR #274](https://github.com/napari/napari-animation/pull/274)

#### Review

Self-review checklist:

* [x] The change is limited to documentation.
* [x] Only `README.md` was modified.
* [x] The documentation wording matches the implementation.
* [x] No unrelated cleanup changes were included.
* [x] The existing programmatic example demonstrates the argument.
* [x] The GUI Save dialog behavior is mentioned.
* [x] The default GUI state is documented.
* [x] The formatting matches the existing README style.
* [x] The PR references and closes the original issue.
* [x] Maintainer feedback was addressed.
* [x] The duplicate example and separate verbose section were removed.

#### Evaluate

I verified the contribution by:

* searching the updated README for `canvas_only`
* reviewing the Markdown structure
* confirming the explanation covers GUI and programmatic use
* reviewing the final Git diff
* confirming that only `README.md` changed
* confirming that the branch has no merge conflicts
* confirming that the `pre-commit.ci` check passed
* reviewing the updated pull request after pushing the revision

---

## Testing Strategy

### Unit Tests

Not applicable because this is a documentation-only change and no application behavior was modified.

### Integration Tests

Not applicable because no production logic or integration behavior was changed.

### Automated Checks

* [x] `pre-commit.ci` completed successfully.
* [x] The pull request has no merge conflicts.
* [ ] One repository workflow is awaiting maintainer approval.

### Manual Testing

Manual verification completed:

* [x] Searched the codebase for `canvas_only`.
* [x] Reviewed `animation.py` for the API parameter and default value.
* [x] Reviewed `savedialog_widget.py` for the GUI checkbox behavior.
* [x] Reviewed rendering-related source code.
* [x] Confirmed `docs/index.md` includes `README.md`.
* [x] Reviewed the initial README diff before committing.
* [x] Reviewed the maintainer-feedback revision diff before committing.
* [x] Confirmed only `README.md` was changed.
* [x] Removed wording that was not supported by the implementation.
* [x] Confirmed the existing scripting example demonstrates programmatic use.
* [x] Confirmed the final explanation covers both `True` and `False` behavior.
* [x] Confirmed the separate verbose subsection was removed.

---

## Implementation Notes

### Phase II: Reproduce and Plan

For Phase II, I confirmed that this issue was a documentation gap rather than a functional defect. I reproduced the problem by locating the existing `canvas_only=False` scripting example in the README and confirming that no explanation of the argument was provided.

I traced the option through the API and GUI code to understand its behavior. I identified `README.md` as the correct file to update because `docs/index.md` includes it in the rendered documentation.

Before implementing the change, I planned to:

1. Explain the behavior of `canvas_only=True`.
2. Explain the behavior of `canvas_only=False`.
3. Connect the programmatic option to the GUI **Canvas only** checkbox.
4. Keep the change limited to documentation.
5. Verify the wording against the implementation.
6. Review the final diff before committing.

**Phase II status:** Complete.

### Week 1 Progress

During Week 1, I:

* selected napari-animation issue #235
* reviewed the issue description
* forked and cloned the repository
* created and pushed a working branch
* searched the codebase for `canvas_only`
* reviewed the relevant API and GUI source files
* identified the correct documentation location
* wrote a solution plan
* implemented the initial documentation update
* manually reviewed the final diff
* committed and pushed the change
* opened pull request #274 to the upstream repository

### Maintainer Review Progress

The maintainer reviewed the initial pull request and explained that the separate **Canvas only** subsection was too verbose. They recommended:

* removing the sentence introducing a second programmatic example
* moving the explanation closer to the existing `animation.animate(...)` call
* placing the GUI Save dialog explanation below the existing script
* reducing repeated information
* keeping the documentation aligned with the project’s AI-assisted contribution policy

I revised the README by:

* removing the separate subsection
* removing the duplicate programmatic example
* replacing approximately 20 lines of documentation with a concise explanation
* placing the final explanation immediately below the existing scripting example
* keeping the update limited to `README.md`
* pushing the revision to the same branch and pull request

### Code Changes

* **Files modified:** `README.md`
* **Initial commit:** [ADD INITIAL COMMIT URL HERE]
* **Revision commit:** [ADD REVISION COMMIT URL HERE]
* **Working branch:** [docs/canvas-only-kwarg](https://github.com/pals6/napari-animation/tree/docs/canvas-only-kwarg)
* **Approach decisions:** I kept the PR documentation-only, avoided unrelated docstring changes, removed the unsupported `scale_factor` explanation, and revised the documentation to match the maintainer’s preference for concise wording integrated with the existing example.

---

## Pull Request

**PR Link:** [napari-animation PR #274](https://github.com/napari/napari-animation/pull/274)

### Initial PR Description

The original pull request added a separate **Canvas only** section explaining:

* what `canvas_only=True` does
* what `canvas_only=False` does
* that `canvas_only=True` is the default
* how the option maps to the GUI Save dialog
* how to use the option programmatically

### Final Implementation

After maintainer review, the separate section was removed.

The final change adds a concise explanation below the existing scripting example:

```markdown
Set `canvas_only=True` to export only the napari canvas, or `False` to include the
full viewer interface. In the GUI Save dialog this corresponds to the **Canvas only**
checkbox, which is enabled by default.
```

### Maintainer Feedback

* **Reviewer:** Tim Monko
* **Feedback:** The initial documentation overexplained information already available in the scripting example. The reviewer recommended removing the separate introductory sentence and duplicate example, integrating the explanation with the existing `animation.animate(...)` call, and moving the GUI explanation below it.
* **Follow-up request:** The reviewer later asked whether I still intended to continue the pull request and noted that it might be closed if there was no response within one week.
* **Response:** I confirmed that I wanted to continue, apologized for the delayed response, revised the documentation, and pushed the updated commit to the same pull request.
* **Changes made:** Removed the separate subsection and duplicate example, reduced the documentation to a concise explanation below the existing script, and kept the change limited to `README.md`.

### Pull Request Status

**Status:** Maintainer feedback addressed; awaiting follow-up review.

### CI and Merge Status

* `pre-commit.ci`: Passed
* Merge conflicts: None
* Maintainer workflow approval: Pending
* Pull request: Open

---

## Learnings & Reflections

### Technical Skills Gained

I learned how to:

* navigate an unfamiliar open-source Python repository
* search for a parameter across API, GUI, and rendering code
* verify documentation wording against actual implementation behavior
* identify how a project’s documentation pages are assembled
* create a focused Git branch and commits
* submit a pull request to an upstream repository
* respond to real maintainer review feedback
* update an existing pull request by pushing to the same branch
* balance completeness with a project’s preference for concise documentation
* keep a contribution narrowly scoped to the original issue

I also learned that documentation issues can require careful code reading. Even when no functionality is changed, inaccurate or overly verbose documentation can make a contribution less useful.

### Challenges Overcome

One challenge was ensuring that the documentation did not overclaim behavior.

During review, I found that a possible note about `scale_factor` repeated a statement from a docstring that did not appear to match the implementation in `frame_sequence.py`. Instead of including uncertain information, I removed the note.

Another challenge was determining the appropriate level of detail. My initial documentation was accurate but more verbose than the project preferred. The maintainer’s feedback helped me understand that the existing scripting example already provided useful context and only needed a short explanation.

I addressed this by reducing the new documentation from a separate multi-line section to a concise explanation directly below the existing example.

### What I’d Do Differently Next Time

Next time, I would:

* inspect both the implementation and nearby documentation patterns before drafting
* compare the proposed addition with the amount of detail used elsewhere in the README
* begin with the smallest documentation change that fully answers the issue
* document the reproduction and solution plan before implementation
* monitor the pull request more frequently so I can respond to maintainer feedback sooner

### Maintainer Feedback Reflection

The maintainer’s feedback showed me that technically accurate documentation can still be rejected or revised if it does not match the project’s communication style.

The initial version repeated information through:

* a separate heading
* a bullet list
* an additional programmatic example
* explanatory prose

The revised version reused the existing example and added only the missing explanation. This made the documentation more consistent with the project and easier to review.

---

## Resources Used

* [napari-animation issue #235](https://github.com/napari/napari-animation/issues/235)
* [napari-animation pull request #274](https://github.com/napari/napari-animation/pull/274)
* [napari-animation upstream repository](https://github.com/napari/napari-animation)
* [My fork: pals6/napari-animation](https://github.com/pals6/napari-animation)
* [Working branch: docs/canvas-only-kwarg](https://github.com/pals6/napari-animation/tree/docs/canvas-only-kwarg)
* `README.md`
* `docs/index.md`
* `napari_animation/animation.py`
* `napari_animation/_qt/savedialog_widget.py`
* `napari_animation/viewer_state.py`
* `napari_animation/frame_sequence.py`
* napari AI contribution policy referenced by the maintainer

---

## AI Usage Log

### Tools Used

* Codex
* Claude Code
* ChatGPT

### How AI Helped

Codex helped inspect the repository and identify where `canvas_only` appeared in the codebase and documentation.

Claude Code reviewed the documentation diff against the implementation and identified that a proposed `scale_factor` note repeated a docstring claim that did not appear to match the actual code. It also helped prepare the minimal revision after maintainer feedback.

ChatGPT helped:

* evaluate the issue as a first open-source contribution
* plan the contribution workflow
* draft the initial issue comment
* prepare repository investigation prompts
* structure the Phase II reproduction and solution plan
* prepare the pull request description
* interpret the maintainer’s review feedback
* plan the revision and follow-up response
* organize this contribution log

### How I Verified AI Output

I manually reviewed:

* the relevant source files
* the existing README
* the documentation structure
* the initial Git diff
* the revised Git diff
* the list of modified files
* the wording describing `canvas_only=True` and `canvas_only=False`
* the maintainer’s exact review comments
* the pull request status after pushing the revision

I confirmed that only `README.md` was changed and removed wording that was unsupported or unnecessarily repetitive.

### Reflection

AI helped reduce the time required to navigate an unfamiliar repository and review the documentation. However, I remained responsible for every claim included in the contribution.

The maintainer feedback reinforced that AI-generated or AI-assisted text must be carefully adapted to the project’s existing style. The final version became stronger after I reduced the generated explanation and followed the maintainer’s preference for a smaller, more direct change.
