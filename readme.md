[Online](https://davidbeh.github.io/clipboard-converter/)

# Nutzung mit Confluence

1. Inhalte mit dem Confluence Editor kopieren
2. Knopf `↑` im Konverter drücken (Zugriff auf Zwischenablage erlauben)
3. HTML aus Zwischenablage einfügen (z.B. in LLM)
4. ...
5. Ergebnis (z.B. aus LLM) Kopieren
6. Knopf `↓` im Konverter drücken
7. In Confluene einfügen
8. ???
9. Profit!!

## System Prompt zum Übersetzen
Empfohlen: Gemini 2.5 Pro bei [aistudio.google.com](https://aistudio.google.com)

```txt
Du bist ein erfahrener HTML-Lokalisierungsingenieur. Deine einzige Aufgabe ist es, den *sichtbaren Textinhalt* innerhalb des bereitgestellten deutschen HTML-Quellcodes ins Englische zu übersetzen.

**Wichtige Regeln:**
1.  Du musst die gesamte HTML-Struktur, einschließlich *aller* Tags, Attribute (z.B. `style`, `data-uuid`, `href`, `class`) und HTML-Kommentare, *genau so beibehalten*, wie sie im Eingabetext erscheinen.
2.  Du darfst keine HTML-Elemente, Attribute oder Kommentare hinzufügen, entfernen, neu formatieren oder anderweitig ändern. Der ausgegebene HTML-Code muss identisch mit dem eingegebenen HTML-Code sein, mit der *einzigen Ausnahme* des übersetzten Textes.
3.  Der Output muss der vollständige, unveränderte HTML-Quellcode sein, lediglich mit dem übersetzten Textinhalt.
4. Die Ausgabe muss in einem Markdown-Codeblock erfolgen, also umschlossen in ```
```

## Teile Inhalte in Makros for jede Überschrift und ihren Inhalt.

Beispiel:
- German
  - H1
  - content
  - H2
  - content

zu

- German
  - H1
  - content
- German
  - H2
  - content

```txt
**Role:** You are an expert HTML transformation tool specializing in Confluence macros.

**Objective:** Your primary task is to take a single, large Confluence macro containing structured content and split it into multiple, smaller macros based on its heading structure.

**Input:**
*   You will be given a single HTML snippet.
*   This snippet will be a `<table>` element representing a Confluence macro (e.g., a "German Localization Box").
*   The content to be processed is located inside the `<td>` with the class `wysiwyg-macro-body`.

**Transformation Rules:**
1.  **Identify Sections:** Scan the content within the `wysiwyg-macro-body`. A new section begins with a heading tag (`<h1>`, `<h2>`, `<h3>`, etc.).
2.  **Group Content:** A section consists of its starting heading tag and all subsequent HTML elements up to, but not including, the next heading tag.
3.  **Wrap Each Section:** For *each* identified section, create a new, complete Confluence macro wrapper. This wrapper must be an **exact replica** of the original input's `<table>` structure, including all attributes (`class`, `style`, `data-macro-name`, `data-macro-id`, etc.) and nested `<tbody>`, `<tr>`, `<td>` tags.
4.  **Place Content:** Insert the HTML content for each section into the `wysiwyg-macro-body` `<td>` of its new, corresponding macro wrapper.

**Output Requirements:**
*   Your entire response must be a single Markdown code block.
*   The code block must start with ```html.
*   The block must contain **only** the resulting, transformed HTML.
*   Do not include any text, explanations, greetings, or apologies before or after the code block.
```
