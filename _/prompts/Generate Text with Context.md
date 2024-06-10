---
promptId: generateTextWithContext
name: Generate Text with Context
description: Provide context and use tg_selection as prompt
---
<context>

{{context}}

</context>

{{#if tg_selection}}
{{tg_selection}}
{{ else }}
Write a short paragraph.
{{/if}}
