# 🎤 Pinyin Lyric Sheet · 拼音歌词

**Turn any Mandarin song into a big, printable lyric sheet with pinyin above every character.**

Paste the lyrics, type (or auto-fill) the pinyin, choose how many pages you want, and print. The text grows to fill the pages, so it stays easy to read while you sing.

---

## ✨ Features

**Lyrics**
- Paste lyrics straight from Google or any lyrics site
- Works with **Simplified 简体** and **Traditional 繁體** characters
- Each character gets its own pinyin box. Punctuation, spaces and English words are left alone
- Editing the lyrics keeps the pinyin you've already typed

**Typing pinyin**
- Tone numbers become tone marks: `ni3` → **nǐ**, `lv4` → **lǜ**
- Jumps to the next character after you type a tone number (you can turn this off)
- Full keyboard navigation (see shortcuts below)
- **✨ Auto-fill**: fills empty boxes with suggested pinyin. It reads whole phrases, so it handles most 多音字 (e.g. 银**行** *háng* vs 行走 *xíng*)

**Printing**
- **Fit to N pages**: pick a page count and the text scales up to fill them
- Live preview that matches the printed output exactly
- A4 or Letter, portrait or landscape
- Margins from Tiny to Normal, left or centred lines
- Print in 简体 or 繁體, whatever was pasted
- Pinyin in red, blue or black, or **hide the pinyin** for a characters-only sheet
- **Download PDF** or **Print** directly

**Everything else**
- UI in **English, Bahasa Indonesia and 中文**
- Your work saves automatically in your browser
- No sign-up, no server, no tracking

---

## ⌨️ Keyboard shortcuts

| Key | Action |
| --- | --- |
| `→` | Next character (when the cursor is at the end of the box) |
| `←` | Previous character (when the cursor is at the start of the box) |
| `↓` / `↑` | Same position on the next / previous line |
| `Space` / `Enter` | Next character |
| `Shift` + `Enter` | Previous character |
| `Backspace` on an empty box | Go back one character |
| `1` `2` `3` `4` | Add that tone mark and move on |
| `5` or `0` | Neutral tone (no mark) |
| `v` | ü |

---

## 🚀 Getting started

There's no build step. The whole app is one `index.html` file.

**Run locally**

```bash
# just open index.html in a browser, or:
npx serve .
```

**Deploy** (any static host works)

| Host | How |
| --- | --- |
| Vercel | `npx vercel` in this folder. Framework: *Other*, no build command |
| Netlify | Drag the folder onto [app.netlify.com/drop](https://app.netlify.com/drop) |
| GitHub Pages | Settings → Pages → deploy from branch `main`, folder `/` |
| Cloudflare Pages | Connect the repo, no build command, output directory `/` |

---

## 🧠 How it works

```
Paste lyrics ──► split into characters ──► pinyin boxes (typed or auto-filled)
                                                    │
                                                    ▼
             PDF / print ◄── canvas pages ◄── layout engine (fits text to N pages)
```

- **Parsing**: each line is split into characters. Chinese characters (including rare CJK extension ranges) get a pinyin box. Everything else is kept as-is.
- **Auto-fill**: traditional text is converted to simplified with `opencc-js` first, because pinyin lookup is more accurate on simplified text, then `pinyin-pro` produces pinyin for the whole line. The original characters are never changed.
- **Layout**: a small layout engine measures every character and pinyin syllable, wraps lines (preferring breaks after punctuation and never starting a line with punctuation), and binary-searches the largest font size that fits your chosen page count.
- **Rendering**: pages are drawn on `<canvas>`. The preview and the PDF share the same drawing code, so what you see is what you print. PDFs are rendered at about 300 dpi with `jsPDF`.
- **Storage**: lyrics, pinyin and settings are kept in `localStorage`, on the visitor's own device only.

---

## 🧰 Tech

Plain HTML, CSS and JavaScript. No framework, no bundler. Libraries load from CDNs:

| Library | Used for |
| --- | --- |
| [pinyin-pro](https://github.com/zh-lx/pinyin-pro) | Auto-fill pinyin |
| [opencc-js](https://github.com/nk2028/opencc-js) | 简体 ↔ 繁體 conversion (the full converter loads only when needed) |
| [jsPDF](https://github.com/parallax/jsPDF) | PDF export |
| [Noto Sans SC / TC / Noto Sans](https://fonts.google.com/noto) | Chinese characters and pinyin tone marks |

> An internet connection is needed on first load to fetch these. After that the page works offline until it's refreshed.

---

## ⚠️ Known limitations

- Auto-fill is dictionary-based. It's accurate most of the time, but songs sometimes bend pronunciation, so give the tricky characters a quick check.
- The PDF contains images of the pages, so its text isn't selectable or searchable. That's on purpose: it guarantees the PDF looks exactly like the preview.

---

## 🗺️ Ideas for later

- [ ] Tone-coloured pinyin (one colour per tone)
- [ ] Save and reload multiple songs
- [ ] Mark sections (Verse, Chorus) and print repeated parts once
- [ ] Share a song via link

---

## 🙌 Credits

Made by [@DesmondInTech](https://desmondintech.page)

Thanks to the maintainers of pinyin-pro, opencc-js and jsPDF.