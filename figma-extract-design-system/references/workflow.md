# Extraction Workflow

Use this order unless the file already has a stable system that only needs minor extension.

1. Review the source screen structure
2. Identify reusable boundaries
3. Split findings into:
   - foundations
   - icons
   - primitive components
   - composed components
   - local-only layout
   - decoration / divider / container
4. Exclude what should not be extracted
5. Present `To Add / To Modify / Do Not Extract`
6. Build or extend foundations
7. Extract icons
8. Extract primitive components
9. Extract composed components
10. Rebind the original screens
11. Normalize spec layout, titles, category groups, and semantic layer naming

## Operating rules

- Do not create components before the review list is confirmed
- Do not group by page when function-based grouping is possible
- Do not leave raw vectors embedded when an icon should be standalone
- Do not stop after building components; rebind the source screens
- Do not normalize spec layout until the component structure is stable

