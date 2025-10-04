# Wikidata Book Itemizer

A simple React + Tailwind web tool to **generate QuickStatements for creating "work" and "edition" items on Wikidata**.  
It helps Wikidata editors quickly create structured items for books, articles, and other written works, with support for multilingual labels, author metadata, publication details, and direct QuickStatements integration.

## ✨ Features

- **Generate two linked items at once**:
  - *Work* item (`instance of: written work` → `Q47461344`)
  - *Edition* item (`instance of: edition` → `Q3331189`)

- **Auto-generated labels and descriptions**:
  - English + your local language (23+ languages supported including Punjabi, Hindi, Urdu, Bengali, Tamil, Spanish, French, Chinese, Arabic, and more)
  - Descriptions like `work by [author]` or `[year] edition of work by [author]`
  - Dynamic placeholders that change based on selected language

- **Punjabi script selection**:
  - Choose between Gurmukhi (ਗੁਰਮੁਖੀ) and Shahmukhi (شاہ مکھی) scripts
  - Automatically adds appropriate script qualifier (P282)

- **Author handling**:
  - Uses **P50 (author)** if Wikidata Q-ID is provided  
  - Falls back to **P2093 (author name string)** if Q-ID is not available
  - Input validation ensures Q-IDs follow correct format (Q + numbers)

- **Publisher support**:
  - Add publisher information via **P123 (publisher)** to edition items
  - Accepts Wikidata Q-ID with format validation

- **Smart ISBN handling**:
  - Automatically determines ISBN format based on publication year
  - **P957 (ISBN-10)** for publications up to 2006
  - **P212 (ISBN-13)** for publications from 2007 onwards

- **Language support**:
  - 23+ languages with proper Wikidata Q-IDs
  - Automatically adds **P407 (language of work)**  
  - Adds **P282 (writing system)** qualifier for Punjabi with script selection

- **Publication metadata**:
  - **P577 (publication date)** - added to edition items only
  - Year-based validation (4 digits only)

- **Dark mode support**:
  - Automatically detects system theme preference
  - Manual toggle available
  - Smooth transitions between light and dark themes

- **One-click workflows**:
  - **Copy** button - instantly copies QuickStatements to clipboard
  - **Create in QuickStatements** button - opens QuickStatements tool with pre-filled commands
  - Direct integration with QuickStatements API (same method as PetScan)

## 🚀 Getting Started

1. Open `https://kuldeepburjbhalaike.github.io/BookItemizer/` in your browser — no build process needed.
2. Fill in the required fields:
   - Book label (English) *required*
   - Author name (English) *required*
   - Optional: Local language labels, author Q-ID, publisher Q-ID, publication year, ISBN
3. Click **"Create in QuickStatements"** to automatically open QuickStatements with your commands pre-loaded, or use **"Copy"** to manually paste them.
4. Login to Wikidata and click "Import" to create both items instantly.

## 📝 Example Output

> **Example:** For a work *Example Book* by *Kuldeep Singh* (Q123456) published by Example Publisher (Q789) in 2025 with ISBN 978-0-123-45678-9, in Punjabi (Gurmukhi script):
>
> ```
> CREATE
> LAST|Len|"Example Book"
> LAST|Lpa|"ਉਦਾਹਰਨ ਕਿਤਾਬ"
> LAST|Den|"work by Kuldeep Singh"
> LAST|Dpa|"ਕੁਲਦੀਪ ਸਿੰਘ ਦੀ ਰਚਨਾ"
> LAST|P31|Q47461344
> LAST|P50|Q123456
> LAST|P407|Q58635|P282|Q689894
> 
> CREATE
> LAST|Len|"Example Book"
> LAST|Lpa|"ਉਦਾਹਰਨ ਕਿਤਾਬ"
> LAST|Den|"2025 edition of work by Kuldeep Singh"
> LAST|Dpa|"ਕੁਲਦੀਪ ਸਿੰਘ ਦੀ ਰਚਨਾ ਦੀ 2025 ਛਾਪ"
> LAST|P31|Q3331189
> LAST|P50|Q123456
> LAST|P407|Q58635|P282|Q689894
> LAST|P123|Q789
> LAST|P577|+2025-00-00T00:00:00Z/9
> LAST|P212|"978-0-123-45678-9"
> ```

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
