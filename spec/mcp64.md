# mcp64 Specification v1.0

## Overview
MCP64 defines the æ state-machine protocol, including allowed transitions and operational limits for executing intents in controlled environments.

## State Transitions

### 1. OPEN
- **Purpose**: Read-only orientation.
- **Allowed Commands**: Navigation and inspection.
- **Requirements**: Cannot modify execution state.

### 2. VERIFY
- **Purpose**: Integrity validation.
- **Allowed Commands**: Hashing and mirror checks.
- **Requirements**: Validation MUST pass.

### 3. ENTER
- **Purpose**: Consent gate for execution.
- **Allowed Commands**: Authorization.
- **Requirements**: Explicit approval is REQUIRED.

### 4. RUN
- **Purpose**: Execute the payload/task.
- **Allowed Commands**: State mutation.
- **Requirements**: ENTER state MUST precede.

### 5. ERROR
- **Purpose**: Terminal state for failures.
- **Allowed Commands**: None.
- **Requirements**: Irrecoverable; rollback.

## Validation Rules
- No skipping states: OPEN → VERIFY → ENTER → RUN.
- No reverse transitions are permitted.
- ERROR is always the final state.

---
MCP64 enforces structural control for all æ execution pathways.