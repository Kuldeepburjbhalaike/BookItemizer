# Wikidata Book Itemizer

A lightweight, standalone React + Tailwind web tool to **generate QuickStatements for creating "Work" and "Edition" items on Wikidata**.  
It simplifies the bibliographic cataloging process by handling multilingual labels, entity linking, author/contributor metadata, publication properties, Wikisource pages, Wikimedia Commons media files, and one-click QuickStatements import.

---

## ✨ Features

- **Dual Creation Modes**:
  - **Create Both (Work & Edition)**: Generates commands to create both a *Work* item (`instance of: written work` → `Q47461344`) and an *Edition* item (`instance of: edition` → `Q3331189`) simultaneously.
  - **Create Only Edition (Work Already Exists)**: Search for an existing work on Wikidata (or input a QID) to extract existing metadata, prefill matching attributes, and link the new edition using **P629 (edition or translation of)**.

- **Smart Work Search & Verification**:
  - Search existing works filtered specifically to written works, literary works, collective works, books, or creative works via SPARQL / Wikidata Action API.
  - Infinite scroll pagination in the dropdown menu.
  - Automatic background verification of work items ensuring `P629` is linked only to valid written/literary work subclasses.

- **Dynamic Multilingual Support**:
  - 23+ languages supported (including Punjabi, Hindi, Urdu, Bengali, Tamil, Telugu, Marathi, Gujarati, Kannada, Malayalam, Odia, Assamese, Sanskrit, and international languages).
  - **"None (English Only)"** option to bypass local language fields when cataloging English-only works.
  - **Dynamic language re-fetching**: Changing the selected local language dynamically re-queries Wikidata to load the corresponding localized title and author names.
  - Punjabi script selection: Gurmukhi (ਗੁਰਮੁਖੀ) vs. Shahmukhi (شاہ مکھی) with **P282** qualifier.

- **Author & Contributor Metadata**:
  - **Author**: Uses **P50 (author)** if a Wikidata QID is selected, falling back to **P2093 (author name string)** if an item does not exist.
  - **Editor (P98)**: Optional search and statement generation for edition items.
  - **Translator (P655)**: Optional search and statement generation for edition items.

- **Publication & Bibliographic Details**:
  - **Title (P1476)**: Auto-generated with native language tagging (falls back to English when "None" is chosen).
  - **Publisher (P123)** & **Place of publication (P291)** with live entity autocomplete search.
  - **Publication Date (P577)** with 4-digit year format.
  - **Number of Pages (P1104)**: Clean integer validation (mandatory).
  - **Wikisource Index Page URL (P1957)**: Mandatory direct link connecting digitized editions.
  - **Smart ISBN Handling**: Automatically chooses **P957 (ISBN-10)** for years up to 2006 or **P212 (ISBN-13)** for 2007 onwards.

- **Wikimedia Commons Integration**:
  - **P996 (Wikimedia Commons File)**: Live search directly against Commons **Namespace 6 (File:)** with image thumbnail previews.
  - **P4714 (Title Page Number)**: Optional qualifier added to P996 when a specific title page is specified.

- **Streamlined Workflow & Dark Mode**:
  - Auto-generated natural language descriptions in English and native scripts (e.g., Punjabi `ਦੀ ਰਚਨਾ`, Hindi `की रचना`, Urdu `کی تخلیق`, Bengali `-এর কাজ`).
  - Automatic system dark mode detection with manual toggle.
  - **Copy** button and **Create in QuickStatements** button for direct import into Toolforge.

---

## 🚀 Getting Started

1. Open the live tool in your browser: [https://kuldeepburjbhalaike.github.io/BookItemizer/](https://kuldeepburjbhalaike.github.io/BookItemizer/) *(no installation or build steps required)*.
2. Choose your mode:
   - **Create Both (Work & Edition)**: If starting from scratch.
   - **Create Only Edition (Work Already Exists)**: If the work item is already present on Wikidata.
3. Fill in the required fields (`*`):
   - **Label (English)**
   - **Label in Local Language** *(unless "None" is chosen)*
   - **Author Name (English)**
   - **Author Name in Local Language** *(unless "None" is chosen)*
   - **Number of Pages (P1104)**
   - **Wikisource Index Page URL (P1957)**
4. *(Optional)* Add Publication Year, Publisher, Place, ISBN, Editor, Translator, or Wikimedia Commons File.
5. Click **"Create in QuickStatements"** to import directly, or **"Copy"** to paste commands manually into QuickStatements.

---

## 📝 Example Output

### Mode: Both (Work & Edition)
```text
CREATE
LAST|Len|"Example Book"
LAST|Lpa|"ਉਦਾਹਰਨ ਕਿਤਾਬ"
LAST|Den|"work by Author Name"
LAST|Dpa|"ਲੇਖਕ ਦਾ ਨਾਮ ਦੀ ਰਚਨਾ"
LAST|P31|Q47461344
LAST|P50|Q12345
LAST|P407|Q58635|P282|Q689894
LAST|P1476|pa:"ਉਦਾਹਰਨ ਕਿਤਾਬ"

CREATE
LAST|Len|"Example Book"
LAST|Lpa|"ਉਦਾਹਰਨ ਕਿਤਾਬ"
LAST|Den|"2024 edition of work by Author Name"
LAST|Dpa|"ਲੇਖਕ ਦਾ ਨਾਮ ਦੀ ਰਚਨਾ ਦੀ 2024 ਛਾਪ"
LAST|P31|Q3331189
LAST|P50|Q12345
LAST|P407|Q58635|P282|Q689894
LAST|P1476|pa:"ਉਦਾਹਰਨ ਕਿਤਾਬ"
LAST|P123|Q6789
LAST|P291|Q1234
LAST|P577|+2024-00-00T00:00:00Z/9
LAST|P1104|256
LAST|P212|"978-0-123-45678-9"
LAST|P1957|"[https://pa.wikisource.org/wiki/Index:Example.pdf](https://pa.wikisource.org/wiki/Index:Example.pdf)"
LAST|P996|"Example Book.pdf"|P4714|"5"
```

###Mode: Edition Only (Linked to Existing Work Q136290840)
```
CREATE
LAST|Len|"Example Book"
LAST|Lpa|"ਉਦਾਹਰਨ ਕਿਤਾਬ"
LAST|Den|"2024 edition of work by Author Name"
LAST|Dpa|"ਲੇਖਕ ਦਾ ਨਾਮ ਦੀ ਰਚਨਾ ਦੀ 2024 ਛਾਪ"
LAST|P31|Q3331189
LAST|P629|Q136290840
LAST|P50|Q12345
LAST|P407|Q58635|P282|Q689894
LAST|P1476|pa:"ਉਦਾਹਰਨ ਕਿਤਾਬ"
LAST|P1104|256
LAST|P1957|"[https://pa.wikisource.org/wiki/Index:Example.pdf](https://pa.wikisource.org/wiki/Index:Example.pdf)"
```

## 🎨 User Interface

- **Responsive design** - works on desktop, tablet, and mobile
- **Dark mode** - automatic system detection with manual toggle
- **Form validation** - ensures Q-IDs and years are in correct format
- **Dynamic placeholders** - change based on selected language
- **Real-time output** - see generated QuickStatements as you type
- **Clear sections** - organized into Labels, Author, and Publication information

## 🛠️ Tech Stack

- [React 18](https://reactjs.org/) (via CDN)
- [TailwindCSS 3](https://tailwindcss.com/) (via CDN)
- [Babel Standalone](https://babeljs.io/docs/en/babel-standalone) for JSX transformation
- [QuickStatements API](https://quickstatements.toolforge.org/)
- MediaWiki Action API (entity search, label fetch, Commons image query)
- Wikidata Query Service (SPARQL) (hierarchical work subclass queries)

## 🌐 Supported Languages

Punjabi, Hindi, Urdu, Bengali, Tamil, Telugu, Marathi, Gujarati, Kannada, Malayalam, Odia, Assamese, Sanskrit, Spanish, French, German, Chinese, Japanese, Korean, Arabic, Russian, Portuguese, Italian

Each language includes:
- Proper Wikidata Q-ID
- Native script placeholders
- Localized description patterns (where applicable)

## 📌 Notes

- **No installation required** - runs entirely in the browser
- **Input validation** - Q-IDs must start with 'Q' followed by numbers
- **Year validation** - Publication year limited to 4 digits
- **ISBN auto-detection** - Format automatically determined by publication year
- **Edition-only properties** - Publisher (P123), publication date (P577), and ISBN are only added to edition items
- **Multilingual support** - Descriptions in Punjabi/Hindi/Urdu follow natural language patterns (e.g., `ਦੀ ਰਚਨਾ`, `की रचना`, `کی تخلیق`)

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs or suggest features via GitHub Issues
- Submit pull requests for improvements
- Add support for additional languages

## 👨‍💻 Credits

Made with ❤️ by [Kuldeep](https://meta.wikimedia.org/wiki/User:Kuldeepburjbhalaike)

## 📄 License

MIT License. Free to use and modify.

---

**Quick Links:**
- [Live Tool](https://kuldeepburjbhalaike.github.io/BookItemizer/)
- [QuickStatements](https://quickstatements.toolforge.org/)
- [Wikidata](https://www.wikidata.org/)
