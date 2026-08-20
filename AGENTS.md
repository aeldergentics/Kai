# AGENTS.md

## KaiSkills Sandbox Architecture

This repository operates within the KaiSkills sandbox environment. Autonomous agents interacting with this codebase must adhere to the standardized protocols and execution parameters described below.

---

## Primary CLI Entry Point

All interaction with KaiSkills management tools must be executed via the primary CLI entry point:

```bash
python /root/kai_skills/manager.py
```

Do not attempt to execute skill management operations by directly invoking individual internal sub-scripts unless instructed by the primary CLI manager.

---

## Querying `registry.json` and Fuzzy Matching Interface

The KaiSkills registry contains available tools, skills, and configuration specifications stored in `registry.json`.

### Query Protocol

1. **Registry Path**: The canonical skill index is located at `/root/kai_skills/registry.json`.
2. **Fuzzy Matching Query Interface**:
   - Query skills and commands using the manager's fuzzy matching interface to resolve skill identifiers, keywords, and action targets.
   - Example command syntax:
     ```bash
     python /root/kai_skills/manager.py query --fuzzy "<search_term>"
     ```
   - Always verify the returned candidate skill entry before invocation.

---

## Parameter Passing & JSON Formatting Standards

When passing parameters into Alpine sandbox tools and KaiSkills utilities, strict JSON formatting standards are required.

### Standards Checklist

- **Valid JSON Format**: All input payloads must be valid, strict JSON objects. Single quotes `'` around keys or values are disallowed; use double quotes `"` exclusively.
- **Escape Sequences**: Properly escape special characters (e.g., quotes `\"`, backslashes `\\`, and newlines `\n`) within JSON string values.
- **CLI String Escaping**: When passing JSON string arguments via bash command lines, wrap the payload in single quotes to protect inner double quotes:
  ```bash
  python /root/kai_skills/manager.py run --skill <skill_name> --params '{"param1": "value1", "param2": true}'
  ```
- **Type Compliance**: Ensure data types conform exactly to the expected parameter schema (e.g., booleans as `true`/`false`, numbers as unquoted numeric literals).

---

## General Agent Directives

1. **Deterministic Execution**: Execute commands deterministically and unambiguously.
2. **Read-only Verification**: After modifying files or executing actions, always verify outcomes using read-only operations.
3. **Repository Conventions**: Follow project style guidelines and check formatting with `./gradlew spotlessCheck` when modifying codebase files.
