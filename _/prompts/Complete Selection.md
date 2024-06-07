---
promptId: completeSelection
name: Complete Selection
description: Complete the selected text (under tg_selection)
---
```json:form
{
  "properties": {
	"maxWords": {
	  "type": "string",
	  "title": "Maximum words",
	  "default": "50"
	}
  },
  "formData": {
	  "maxWords": "50"
  },
  "uiSchema": {
	  "maxWords": {
		"ui:widget": "text",
		"ui:autofocus": true,
	},
  }
}
```
***
Complete the following text in maximum {{ maxWords }} words. Start right where the text ends, as we are going to append it right at the end of the current text. If your reply begins with the text below I will be really mad. 

Text: 
{{tg_selection}}
***
{{output}}