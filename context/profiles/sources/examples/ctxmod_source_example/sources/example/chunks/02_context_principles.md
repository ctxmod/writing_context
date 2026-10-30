Density aligns with how files load: files loaded automatically must be
sparse — every token counts against the agent's budget — while files
read deliberately can be dense. When content exists in a file, reference
that file instead of copying it: a reference consumes fewer tokens than
the content it points to and maintains a live connection, while pasted
content is a drifting snapshot. Shared context files assume nothing
about the consumer's work beyond what the file path declares, and every
edit lands in exactly one layer — shared content for changes that
benefit every consumer, device-local content for workspace-specific
material that is never implicitly promoted.
<ctxmod_locator>context principles</ctxmod_locator>
