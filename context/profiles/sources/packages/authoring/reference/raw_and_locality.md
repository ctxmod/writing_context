# Raw Material and Locality

Sources follow the ordinary `context`/`context.local` rule: authored
content defaults to shared `context/`; an explicitly device-local
override is written to `context.local/`.

## The committed-raw-source rationale

A source — `raw/` included — belongs in committed, shared context when
its content is likely to be requested *for verification* and is not
retrievable from a public location. The test is **verifiability
demand**:

- Share: a PDF worth presenting so a citing claim can be checked
  against the original.
- Do not store raw: a large dataset or schema whose value beyond its
  extracted chunks and summaries is nil, or that no reader will request.
- Local: binaries that are the device-private part of an otherwise
  shared source.

## Locality rules that bind here

- Nothing under `context.local/` is copied into `context/` merely by
  being cited, selected, or rendered; moving it is deliberate promotion.
- Shared sources never depend on local sources — a shared citation
  graph must resolve in the shared-only projection.
- Local sources may cite shared sources freely.

## What raw is for the tool

`raw/**` is never scanned for citations, locators, or components. It is
data. The tooling sees it only as payload with a path; anything a
citation should reach must live in scanned directories.

See also [sources layout](sources_layout.md).
