# Build Verification Log

This is a static build log captured on 2026-03-16. For independent verification,
clone this repo and run `cd lean && lake build`.

## Environment

- **Lean:** 4.24.0 (aarch64-unknown-linux-gnu, commit 797c613eb9b6, Release)
- **Date:** 2026-03-16T02:12:03Z
- **Platform:** Linux 6.14.0-1015-nvidia aarch64

## Build Output

```
Build completed successfully (3106 jobs).
Exit code: 0
```

The build compiled all 15 StackTheory source modules plus 2 Core dependencies
plus Mathlib v4.24.0 (3106 total jobs). All modules built without errors or warnings.

## Sorry Count

```bash
$ grep -rn "sorry" HeytingLean/StackTheory/ HeytingLean/Core/ | wc -l
0
```

Zero `sorry` or `admit` in all source files.

## Note

This project does not use CI/CD. The build log is provided as a static artifact
for transparency. Independent verification is encouraged: clone and build.

A `lakefile.lean` fix was applied in the same commit as this log: the original
`srcDir := "HeytingLean"` caused double-nesting of the module path. Changed to
`srcDir := "."` and added a root `HeytingLean.lean` re-export file to match the
library target name.
