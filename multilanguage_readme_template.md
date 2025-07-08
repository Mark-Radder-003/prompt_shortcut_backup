
# Multi-language README Generation Template

**Usage:**
```
@_prompt/multilanguage_readme_template.md

this repo: **{ @your repo path}**
target language: **{e.g., ja, ko, zh}**
```

---

I want you to help me add multi-language support to the specified repository.

Your task is to read the `README.md` file from the repository path provided above and create a new, translated version of it in the specified target language.

**Requirements:**

**(This is a Must)0.add a `language switcher` on top of all README.md in the specified repository**
    * like " *🌐 Languages: [English](README.md) | [日本語](README_ja.md)*"

1.  **Read the original:** First, read the content of the `README.md` file in the specified repository.
2.  **Translate the content:** Translate the entire content of the `README.md` into the `{target language}`.
3.  **Create a new file:** Save the translated content into a new file. The new file should be named `README_{target language}.md`. For example, if the target language is `ja`, the new file should be `README_ja.md`.
4.  **Do not modify the original:** It is critical that you do not change the original `README.md` file in any way.
5.  **Maintain formatting:** Preserve the original Markdown formatting (headings, lists, code blocks, links, etc.) in the translated file.

