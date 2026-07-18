# Confidence Levels

Use these confidence levels when recording findings or proposed changes.

- `high`: The pattern appears 3+ times across source screens with clear visual and structural evidence.
- `medium`: The pattern appears 2 times, or partial style differences need human confirmation.
- `low`: The pattern appears once or is based on inference. Default to not acting and ask first.

When the same pattern is visually contradictory across screens, such as the same button styled differently, cap confidence at `medium` or lower and surface the conflict to the user instead of picking a side.
