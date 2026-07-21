# Cursor context controls

## Method

Use surgical `@code`/`@file` context and name exact symbols and paths. Avoid broad `@folder` injection unless the folder is truly the needed evidence. Keep rules concise; referenced files in rules add context too.

## Caution

Cursor documentation warns that folder inclusion can include full contents and, particularly in Max mode, use the model’s full context window and increase cost. Start from automatic discovery plus narrow references rather than manually attaching a repository.

## Sources

- [Working with context](https://docs.cursor.com/en/guides/working-with-context)
- [`@folders` behavior](https://docs.cursor.com/context/%40-symbols/%40-folders)
- [Rules](https://docs.cursor.com/context/rules)
