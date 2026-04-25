# Clinic Rubric v0

This rubric is shared across the `clinic` evaluation suite.

## Core Metrics

### 1. Trigger Precision

Question:
Should `clinic` activate for this input?

Scoring:

- `1`: correct activation decision
- `0`: wrong activation decision

### 2. Mode Accuracy

Question:
If `clinic` activates, did it choose the correct mode?

Allowed labels:

- `审视`
- `求助`
- `决策`
- `开放`

Scoring:

- `1`: exact match
- `0`: mismatch

### 3. Doctor Selection Accuracy

Question:
Did the selected roster cover the required viewpoints?

Scoring:

- `2`: strong match; selected doctors fit the need and include useful tension
- `1`: acceptable but weak; mostly relevant, but roster lacks contrast or misses one key angle
- `0`: poor match; roster is redundant, flattering, or misses the task entirely

### 4. Persona Separation

Question:
Do the doctors sound meaningfully different in framework and advice?

Scoring:

- `2`: clearly distinct
- `1`: partially distinct
- `0`: flattened into generic assistant voice

### 5. Summary Fidelity

Question:
Does the host summarize what the doctors actually said?

Scoring:

- `2`: accurate and specific
- `1`: mostly accurate but partially flattened
- `0`: invents consensus, loses key points, or distorts the outputs

### 6. Disagreement Preservation

Question:
When doctors disagree, does the host preserve that disagreement instead of compressing it away?

Scoring:

- `2`: disagreement is explicit and useful
- `1`: disagreement is mentioned but softened
- `0`: disagreement is erased

### 7. Actionability

Question:
If the mode calls for action, is the final prescription concrete enough to use?

Scoring:

- `2`: clear next steps
- `1`: somewhat useful but vague
- `0`: generic advice

### 8. Multi-turn Coherence

Question:
Across multiple rounds, does the host keep the real thread of the conversation instead of resetting or drifting?

Scoring:

- `2`: coherent across turns
- `1`: mostly coherent but loses one important thread
- `0`: resets, drifts, or contradicts earlier context

### 9. Mode Transition Correctness

Question:
When the user follows up, does the host keep or change modes correctly?

Scoring:

- `2`: correct transition or correct non-transition
- `1`: understandable but weak choice
- `0`: clear mode error

### 10. Context Compression Integrity

Question:
After several rounds, if context is summarized, are the right conflict points preserved?

Scoring:

- `2`: preserves the real conflict and decision points
- `1`: preserves some but drops an important distinction
- `0`: compresses away the actual issue

### 11. Host Failure Resistance

Question:
Does the host avoid predictable synthesis failures under adversarial or ambiguous cases?

Scoring:

- `2`: explicitly avoids the target failure and preserves the important distinction
- `1`: partially avoids the failure but still softens or blurs one key distinction
- `0`: falls into the target failure mode

## Failure Modes to Watch

- Over-triggering on generic help-seeking language
- Misclassifying decision problems as general confusion
- Choosing doctors that all reinforce the user's current stance
- Losing adversarial tension in the final summary
- Giving a fake "balanced" conclusion that no doctor actually argued for
- Asking for roster confirmation when direct execution would have been better
- Forgetting what the user was actually asking after a follow-up turn
- Changing to the wrong mode after the user clarifies or narrows the issue
- Compressing multi-turn context into generic therapy language
- Creating fake consensus where doctors actually disagreed
- Turning competing explanations into a single smooth story
- Ignoring the latest user-provided evidence
- Turning open discussion into a forced conclusion
- Turning help-seeking into a generic action checklist
- Replacing a decision framework with "follow your preference"

## Output Recording Template

Suggested columns:

- `case_id`
- `activated`
- `expected_activate`
- `predicted_mode`
- `expected_mode`
- `selected_doctors`
- `doctor_selection_score`
- `persona_separation_score`
- `summary_fidelity_score`
- `disagreement_preservation_score`
- `actionability_score`
- `multi_turn_coherence_score`
- `mode_transition_score`
- `context_compression_score`
- `host_failure_resistance_score`
- `notes`
