# Confidence Levels

Use these confidence levels when recording findings or proposed changes.

- `high`: The pattern appears 3+ times across source screens with clear visual and structural evidence.
- `medium`: The pattern appears 2 times, or partial style differences need human confirmation.
- `low`: The pattern appears once or is based on inference. Default to not acting and ask first.

## Independence rule

Occurrences only count when they are independent. State copies of the same screen (base vs overlay, base vs modal, guided-tour duplicates), duplicated frames, and repeated rows inside one list are each ONE occurrence, not several. Before counting, check whether two occurrences share the same origin; if they do, collapse them into one.

When the same pattern is visually contradictory across screens, such as the same button styled differently, cap confidence at `medium` or lower and surface the conflict to the user instead of picking a side.
