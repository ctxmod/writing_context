---
description: >-
  Execute a single bounded step that edits a context tree (a module's
  context/ or its context.local/ overlay): authoring or editing
  profiles, packages, rules, reference, skills, agents, and tools,
  with source-versus-override discipline.
binds_to_depth: procedure
---

# Context-Editing Procedure

Execute a single, bounded step that touches a context tree: authoring
or editing profiles, packages, rules, reference, skills, agents, and
tools. The procedure-depth agent takes a delimitated edit specification
(target path, change description, source-versus-override decision) and
produces the file change. Unlike objectives, which determine WHAT change
is needed and WHY, procedures determine HOW the edit is applied.

## Surfacing External Context

Where the environment offers discovery tools for external context (a
search over off-the-shelf MCP servers or agent skills by capability or
keyword, and a read of a candidate's full detail: install and
configuration, transport, authentication, tool inventory), use them to
surface reusable external context relevant to the change at hand. Do
not install or wire anything: surface the candidates and their detail;
the caller decides adoption.

## Core Behavior

1. **Classify the edit**: apply the source-versus-override discipline
   (the `place_content_in_its_layer` rule and the editing-layers
   reference of this module's `core` profile):
   - Source edit: the change benefits all consumers → edit the shared
     source (the module's committed `context/` tree, or the upstream
     module that publishes the content).
   - Local override: a project- or device-specific customization of
     shared content → place it in `context.local/`, mirroring the
     shared logical path.
   - Add-only: new content with no shared counterpart → create it under
     the consuming project's own context root at the appropriate path.
2. **Apply layer rules**: decide which layer a given file belongs to
   before editing. Rendered or generated output (a render target
   directory, an agent host's generated context files) is never edited
   directly; change the source and render again.
3. **Author content**: follow this module's principles for structure,
   generalization, and density when authoring new content.
4. **Verify**: confirm the edit lands in the correct layer, that
   `ctxmod vet --root <repository root>` passes clean, and that a render
   of the affected selection stays byte-stable where nothing was meant
   to change.
5. **Return**: a brief summary (2-3 sentences) with the output path; do
   not return full content.

## Tool Constraints

**Allowed**:

- Read: existing context files, shared sources, schema references
- Glob: file discovery for verification
- Grep: content search across the context trees and shared sources
- Write: the target file at the resolved layer (shared source,
  `context.local/` override, or add-only path)
- Edit: existing files at the resolved layer

**Forbidden**:

- Editing rendered or generated output directly
- Launching sub-agents
- Deciding artifact type or output layer (objective-scope decisions)
- Installing or wiring external MCP servers or skills surfaced through
  research

## Parent-Layer Dispatch

This procedure is dispatched by a context-editing objective, when one
exists, or directly by the main or workflow agent. The parent agent
determines WHAT edit is needed; this procedure executes HOW the edit is
applied.

Ad-hoc procedure-depth agents may also load this skill for general
context-editing step mechanics.

## Cross-Cutting Reference

- The single-source-of-truth principle (the `engineering` module's `principles` profile).
- Context efficiency: `context_efficiency.md` in the `density` package of this module's `core` profile.
