Check work quality after major changes by:

1. Parse optional arguments from $ARGUMENTS
   - If no arguments, ask user for preferences
   - Support: --python, --react, --typescript, --rust, --cpp, --all
   - Support: --tests, --lint, --full

2. Interactive options if no arguments provided:
```
🔍 WORK CHECK OPTIONS
━━━━━━━━━━━━━━━━━━━━━━

Which languages to focus on?
1) Python
2) React/JavaScript
3) TypeScript
4) Rust
5) C/C++
6) All languages
> [Wait for selection]

What checks to perform?
a) Unit tests only
b) Linting only
c) Type checking only
d) Full check (tests + lint + types)
e) Quick check (modified files only)
> [Wait for selection]

Additional options?
- Check cross-language integrations? (y/n)
- Include performance benchmarks? (y/n)
- Generate coverage report? (y/n)
```

3. Execute selected checks based on user choices:
```
🎯 CUSTOMIZED WORK CHECK
━━━━━━━━━━━━━━━━━━━━━━━━

Selected: [User's choices]

✓ What might this have broken?
  - Focusing on: [Selected languages]
  - Check depth: [Selected level]

📖 Reading modified files:
  [Filter by selected languages]
```

4. Language-specific execution:
```
FOR PYTHON (if selected):
- Tests: pytest -v
- Lint: pylint, black --check
- Types: mypy --strict

FOR REACT/JS (if selected):
- Tests: npm test -- --coverage
- Lint: eslint src/
- Format: prettier --check

FOR TYPESCRIPT (if selected):
- Compile: tsc --noEmit
- Strict: tsc --strict
- Lint: eslint *.ts

FOR RUST (if selected):
- Tests: cargo test
- Lint: cargo clippy -- -D warnings
- Format: cargo fmt --check

FOR C/C++ (if selected):
- Tests: ctest / make test
- Analyze: clang-tidy
- Check: cppcheck --enable=all
```

5. Provide focused report:
```
## Targeted Work Quality Report

### Scope
- Languages checked: [Selected only]
- Check types: [Selected only]
- Files analyzed: X files

### Results for [Each selected language]
- Test results (if requested)
- Linting issues (if requested)
- Type errors (if requested)

### Quick Summary
✅ PASSED: [What's working]
⚠️ WARNINGS: [Non-critical issues]
❌ FAILED: [Must fix items]

Continue with fixes? (y/n)
```

6. Remember user preferences:
   - Save to `.claude/check-preferences.json`
   - Use as defaults next time
   - Allow override with arguments