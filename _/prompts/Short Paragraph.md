---
promptId: shortParagraph
name: Write a Short Paragraph
description: Write a short paragraph about the content of the note at hand
---
{{#if yaml.text_gen_prompt}}
{{#if yaml.text_gen_prompt}}
{{ yaml.text_gen_prompt }}
{{ else }}
Write a short paragraph about the following:
{{/if}}

Title: {{title}}
{{#if yaml.description}}
Description: {{ yaml.description }}
{{/if}}

{{#if highlights}}
Highlights
========

{{#each highlights}}
- {{this}}
{{/each}}
{{/if}}

{{#if starredBlocks}}
Notable Sections
=============

{{ starredBlocks }}
{{/if}}
