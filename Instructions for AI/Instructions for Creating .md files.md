**When I command you to create an .md file, you should follow these instructions:**
1. Put a divider above every major headings (except the first heading)
2. When naming the .md file, do not put any underscore (\_) when separating words. Instead, insert a space.
3. Do not repeat the same filename for the heading inside that file

---

# Instructions for Mathematical Notes

Whenever you create, edit, format, or reformat mathematical notes:

1. Read and follow the rules in `LaTeX-Formatting-Instructions.md`.
2. Use standard Markdown and Obsidian-compatible LaTeX.
3. Use `$...$` for inline mathematics and `$$...$$` for display equations.
4. Preserve mathematical accuracy, explanations, examples, and the original meaning.
5. Format headings, lists, tables, equations, and calculations consistently.
6. Verify calculations and check for malformed LaTeX delimiters.
7. Return the complete, properly formatted Markdown content.

For mathematical formatting: [[LaTeX Formatting Instructions]]

---

# Filename and Heading Rules

- Treat the Markdown filename and the document's internal headings as separate elements.
    
- **Do not automatically use the filename as the first heading inside the document.**
    
- Do not create a top-level heading (`#`) that simply repeats the filename.
    
- Begin the document directly with a meaningful introduction, definition, explanation, or other relevant content, unless a heading is necessary for the document's structure.
    
- If an internal heading is needed, choose one that describes the actual content of that section rather than copying the filename.
    
- Do not add redundant headings solely to identify the document's topic when the filename already serves that purpose.
    
- Preserve existing headings when editing a document unless a change is necessary or explicitly requested.
    

### Example

**Filename:**  
`Uses of AI.md`

**Incorrect:**

```
# Uses of AI

Artificial intelligence is used in various fields, including healthcare,
education, finance, transportation, and software development.
```

**Correct:**

```
Artificial intelligence is used in various fields, including healthcare,
education, finance, transportation, and software development.

## Healthcare

AI helps medical professionals analyze medical images, identify patterns,
and support clinical decision-making.

## Education

AI supports personalized learning, automated assessment, and intelligent
tutoring systems.
```

### Exception

If the user explicitly requests a title or a heading matching the filename, follow that request.

**Primary rule:** The filename identifies the document, while internal headings organize its content. Do not duplicate the filename as the first heading unless explicitly requested.