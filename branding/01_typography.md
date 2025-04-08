# Database World Tour - Typography Guidelines

## 1. Philosophy

Our typography system prioritizes clarity, readability, and intellectual rigor. It aims to establish a clear visual hierarchy, support complex technical content, and convey a sense of modern authority suitable for a graduate-level resource. We balance classic legibility with contemporary aesthetics.

## 2. Primary Typeface: Inter

*   **Family**: Inter (Variable Font)
*   **Source**: [Google Fonts](https://fonts.google.com/specimen/Inter)
*   **Rationale**: Inter is a highly versatile sans-serif typeface specifically designed for computer screens. Its large x-height, clean forms, and wide range of weights make it exceptionally readable for both UI elements and long-form text. Its variable nature allows for fine-tuned control over weight and style.
*   **Usage**: Use Inter for all headings, body text, UI elements, captions, and code annotations.

## 3. Secondary Typeface (Code): Source Code Pro

*   **Family**: Source Code Pro
*   **Source**: [Google Fonts](https://fonts.google.com/specimen/Source+Code+Pro)
*   **Rationale**: A monospaced typeface optimized for displaying code snippets. It offers excellent clarity and distinction between similar characters (e.g., O/0, I/l/1), crucial for technical accuracy.
*   **Usage**: Use Source Code Pro exclusively for code blocks and inline code references.

## 4. Typographic Scale & Hierarchy

We use a modular scale based on a root font size of 16px (1rem) for body text to ensure consistent rhythm and hierarchy.

*   **H1 (Page Titles)**: `Inter Bold`, 2.5rem (40px), Line Height 1.2
*   **H2 (Major Sections)**: `Inter Bold`, 2rem (32px), Line Height 1.3
*   **H3 (Sub-Sections)**: `Inter SemiBold`, 1.5rem (24px), Line Height 1.4
*   **H4 (Minor Headings)**: `Inter Medium`, 1.25rem (20px), Line Height 1.4
*   **Body Text**: `Inter Regular`, 1rem (16px), Line Height 1.6
*   **Captions / Small Text**: `Inter Regular`, 0.875rem (14px), Line Height 1.5
*   **Code Blocks**: `Source Code Pro Regular`, 0.9rem (14.4px), Line Height 1.5
*   **Inline Code**: `Source Code Pro Regular`, 0.9rem (14.4px), Background: `#f0f0f0`, Padding: `0.1em 0.3em`
*   **Links**: `Inter Medium`, Inherit size, Color: `#007bff` (or primary brand color), Underline on hover.
*   **Lists (ul/ol)**: Body Text style, appropriate indentation.

## 5. Implementation Notes

*   **Variable Font Usage**: Utilize Inter's variable weights for nuanced control, especially for emphasis (`Inter Medium` or `SemiBold`) within body text where appropriate, but use sparingly.
*   **Line Length**: Aim for an optimal line length of 50-75 characters for body text to enhance readability.
*   **Paragraph Spacing**: Use margin-bottom (e.g., `1rem`) on paragraphs (`<p>`) rather than double line breaks.
*   **Accessibility**: Ensure sufficient color contrast between text and background according to WCAG AA guidelines.
*   **Consistency**: Apply these styles consistently across all documentation, web pages, and presentations associated with the Database World Tour.
