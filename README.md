# Wikidata QuickStatements Generator

A simple React + Tailwind web tool to **generate QuickStatements for creating "work" and "edition" items on Wikidata**.  

It helps Wikidata editors quickly create structured items for books, articles, and other written works, with support for multilingual labels, author metadata, and publication details.

## ✨ Features

- **Generate two linked items at once**:
  - *Work* item (`instance of: written work` → `Q47461344`)
  - *Edition* item (`instance of: edition` → `Q3331189`)
- **Auto-generated labels and descriptions**:
  - English + optional second language (Punjabi, Hindi, Urdu, and more)
  - Descriptions like `work by [author]` or `[year] edition of work by [author]`
- **Author handling**:
  - Uses **P50 (author)** if Wikidata Q-ID is provided  
  - Falls back to **P2093 (author name string)** if not
- **Language support**:
  - Choose from common languages (Punjabi, Hindi, Urdu, Bengali, Tamil, etc.)
  - Automatically adds `P407` (language of work)  
  - Adds `P282` (script) for Punjabi/Gurmukhi
- **Publication year (P577)**:
  - Adds edition-specific publication date if provided
- **One-click copy**:
  - Output QuickStatements are instantly copied to clipboard

## 🚀 Getting Started

1. Clone or download the repository.
2. Open `index.html` in your browser — no build process needed.
3. Fill in:
   - **English label** (required)
   - **Author name** (required)
   - Optional fields: author Q-ID, local language label, publication year.
4. Copy the generated QuickStatements.
5. Paste into [QuickStatements tool](https://quickstatements.toolforge.org/) to create items on Wikidata.

## 📝 Example Output

> **Example:** For a work *Example Book* by *Kuldeep Singh* published in 2025, the generated QuickStatements would look like:
>
> ```
> CREATE
> LAST|Len|"Example Book"
> LAST|Den|"work by Kuldeep Singh"
> LAST|P31|Q47461344
> LAST|P2093|"Kuldeep Singh"
> LAST|P407|Q58635|P282|Q689894
> 
> CREATE
> LAST|Len|"Example Book"
> LAST|Den|"2025 edition of work by Kuldeep Singh"
> LAST|P31|Q3331189
> LAST|P2093|"Kuldeep Singh"
> LAST|P407|Q58635|P282|Q689894
> LAST|P577|+2025-00-00T00:00:00Z/9
> ```

## 🛠️ Tech Stack

- [React](https://reactjs.org/) (via CDN)
- [TailwindCSS](https://tailwindcss.com/)
- [QuickStatements format](https://www.wikidata.org/wiki/Help:QuickStatements)

## 📌 Notes

- Requires only a browser — no installation.
- Supports multilingual workflows for Wikidata book/edition entries.
- Descriptions in Punjabi/Hindi/Urdu follow natural language patterns (e.g., `ਦੀ ਰਚਨਾ`, `की रचना`, `کی تخلیق`).

## 📄 License

MIT License. Free to use and modify.  
