# Skill Test Spec: /setup-engine

## Skill Summary

`/setup-engine` is the Godot-only technical setup entrypoint. It resolves the
pinned Godot version, GDScript baseline, local console executable, engine
reference, runtime check status, and minimal test foundation. It produces one
Godot setup package and asks for one approval before writing all low-risk setup
files in that package.

The skill does not offer Unity or Unreal configuration in this fork.

---

## Static Assertions

- [ ] Has required frontmatter fields: `name`, `description`, `argument-hint`,
  `user-invocable`, `allowed-tools`
- [ ] Has at least two phase headings
- [ ] Contains verdict keywords: `COMPLETE`, `CONCERNS`, and `BLOCKED`
- [ ] Contains package-level approval language before writing setup files
- [ ] Describes Godot-only behavior and rejects multi-engine setup
- [ ] Has a next-step handoff such as `/brainstorm`, `/design-system`,
  `/create-architecture`, or `/smoke-check`

---

## Test Cases

### Case 1: Godot Setup Package

**Fixture:**

- `.codex/docs/technical-preferences.md` exists with placeholders
- `docs/engine-reference/godot/VERSION.md` exists or can be created
- `tests/` is missing
- User provides or project docs contain a Godot 4.x version

**Input:** `/setup-engine`

**Expected behavior:**

1. Skill resolves Godot version from argument, `AGENTS.md`, technical
   preferences, or engine reference.
2. Skill prepares one setup package covering technical preferences, engine
   reference, test foundation, runtime check status, and concerns.
3. Skill asks once to approve the package and planned writes.
4. After approval, Skill writes all low-risk setup files in the package without
   repeated per-file confirmations.
5. Skill returns `COMPLETE` or `CONCERNS` depending on whether `project.godot`
   and console validation are available.

**Assertions:**

- [ ] Engine field is set to Godot 4.x or a pinned Godot version.
- [ ] Language field is GDScript.
- [ ] Godot command is recorded if known.
- [ ] `tests/unit/`, `tests/integration/`, `tests/helpers/`, and `tests/README.md`
  are included when missing.
- [ ] Approval is package-level, not one prompt per file.
- [ ] Verdict is `COMPLETE` or `CONCERNS`.

---

### Case 2: Missing Project File

**Fixture:**

- Godot console executable is known.
- `project.godot` is missing.

**Input:** `/setup-engine`

**Expected behavior:**

1. Skill records runtime check command and status.
2. Skill does not run `--headless --path . --quit` because no Godot project file
   exists.
3. Skill reports the missing project file as a setup concern.

**Assertions:**

- [ ] Runtime check is not falsely reported as passing.
- [ ] `project.godot` missing is named explicitly.
- [ ] Verdict is `CONCERNS`.

---

### Case 3: Multi-Engine Request

**Fixture:**

- User requests Unity, Unreal, or another engine.

**Input:** `/setup-engine unity`

**Expected behavior:**

1. Skill explains this fork is Godot-focused.
2. Skill does not write Unity/Unreal technical preferences.
3. Skill returns `BLOCKED` or a clear redirection.

**Assertions:**

- [ ] No Unity/Unreal routing table is written.
- [ ] Godot-only constraint is stated.
- [ ] No files are changed for the unsupported engine request.

---

## Protocol Compliance

- [ ] Presents the full Godot setup package before asking for approval.
- [ ] Uses one approval for all low-risk setup writes inside the approved package.
- [ ] Runs read-only validation without extra approval when `project.godot` and
  Godot console are available.
- [ ] Does not recommend old multi-engine commands.
- [ ] Ends with a concise setup summary and next step.

