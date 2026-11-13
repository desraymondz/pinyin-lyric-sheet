# Pinyin Lyric Sheet 拼音歌词

Paste Mandarin song lyrics, add pinyin above each character, and print it big.

- Works with Simplified 简体 and Traditional 繁體
- Type `ni3` → `nǐ`, arrow keys to move between characters
- Auto-fill pinyin (runs in the browser, no server)
- Fit to N pages, live preview, download PDF or print
- UI in English, Bahasa Indonesia and 中文

## Run locally

It's a single static file. Open `index.html` in a browser, or serve it:

```bash
npx serve .
```

## Deploy

No build step. Any static host works.

- **Vercel:** `npx vercel` in this folder (framework: Other, no build command)
- **Netlify:** drag this folder onto https://app.netlify.com/drop
- **GitHub Pages:** push to a repo, then Settings → Pages → deploy from branch `main`, folder `/`

## Libraries (loaded from CDN)

- [pinyin-pro](https://github.com/zh-lx/pinyin-pro) for auto-fill
- [opencc-js](https://github.com/nk2028/opencc-js) for 简/繁 conversion
- [jsPDF](https://github.com/parallax/jsPDF) for PDF export
- Noto Sans SC / TC / Noto Sans from Google Fonts

Everything (lyrics, pinyin, settings) is saved in the visitor's own browser via `localStorage`.
