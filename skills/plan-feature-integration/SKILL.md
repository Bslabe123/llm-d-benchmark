---
name: plan-feature-integration
description: Plan and format feature requests for new llm-d features involving inference-perf and llm-d-benchmark.
---

# Plan Feature Integration

## Purpose

Guide the AI in processing a request for a new `llm-d` feature, analyzing its impact on `inference-perf`, and planning its consumption in `llm-d-benchmark`. The output will be an implementation plan and formatted feature requests.

## Usage

```
/feature-request <description of the feature and requirements>
```

## Workflow

### Step 1: Extract Requirements
- Analyze the user's description of the `llm-d` feature.
- Identify the core functionality and top-level requirements.
- Ask clarifying questions if the requirements are ambiguous.

### Step 2: Analyze `inference-perf` Implications
- **Discovery**: Before proposing additions, use available tools (e.g., reading documentation, searching codebase for load generator implementations) to understand the current capabilities of `inference-perf`.
- Determine if `inference-perf` (acting strictly as the core load generator engine) needs:
    - New load generation patterns.
    - New metrics collection or aggregation.
    - Protocol changes or new API support.
- Do *not* plan for `inference-perf` to handle orchestration, deployment, or scenario management.
- Draft a clear feature request for `inference-perf` describing these needs using the template below.

### Step 3: Plan `llm-d-benchmark` Consumption
- Determine how `llm-d-benchmark` (acting strictly as the harness and orchestrator) will consume the new `inference-perf` behavior.
- Identify needed changes to:
    - Scenarios (shell scripts in `scenarios/`).
    - Experiments (YAML configs in `experiments/`).
    - Runner logic or analysis scripts.
- Ensure the plan respects that `llm-d-benchmark` drives the execution flow and deployment.
- Draft a task list or feature request for `llm-d-benchmark` using the template below.

### Step 4: Definition of Ready (Verification)
Before generating the final output, verify that the plan meets these criteria:
- [ ] All new metrics have specified units.
- [ ] Exact CLI flags or environment variables are proposed (no placeholders for names).
- [ ] The files likely to be modified are identified.
- [ ] A mock example of the output (e.g., report section or config) is provided.

### Step 5: Generate Output
- Produce a unified implementation plan detailing the steps above.
- Format the feature requests for both repositories using the templates below.

---

## Feature Request Templates

### inference-perf Feature Request Template
```markdown
## Feature Title

### Description
[Clear description of the requested feature]

### Requirements & Behavior Changes
- [Specific requirement 1]
- [Specific requirement 2]

### Interface Changes (CLI/API)
- Proposed flags: `--example-flag <type>`
- Expected behavior change: [Describe what changes in execution]

### Data Contract (Report Changes)
- Proposed JSON path in results: `$.metrics.new_metric`
- Unit: [e.g., requests/sec, milliseconds]

### Verification Plan
- [How to verify this feature works in isolation]
```

### llm-d-benchmark Feature Request Template
```markdown
## Feature Title

### Description
[Clear description of the requested feature]

### Requirements & Integration
- [Specific requirement 1]
- [Specific requirement 2]

### Configuration Changes
- Proposed environment variables: `LLMDBENCH_NEW_VAR`
- Mapping to `inference-perf` flags: `LLMDBENCH_NEW_VAR` -> `--example-flag`

### Scenario/Experiment Changes
- [Describe needed changes to scenarios or experiment templates]

### Verification Plan
- [How to verify this feature works end-to-end]
```
