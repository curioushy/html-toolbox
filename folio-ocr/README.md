# folio-ocr — vendored dependencies

Static assets for the `folio-ocr.html` tool. All files are hosted here so the tool
works fully offline after first load (no CDN dependency).

## Contents

| File | Size | Purpose | Source | License |
|---|---|---|---|---|
| `tesseract.min.js` | ~60 KB | Tesseract.js main library | [tesseract.js@5.1.1](https://www.npmjs.com/package/tesseract.js) | Apache 2.0 |
| `worker.min.js` | ~120 KB | Tesseract.js worker script | tesseract.js@5.1.1 | Apache 2.0 |
| `tesseract-core-simd.wasm.js` | ~4.6 MB | WASM loader (SIMD build) | [tesseract.js-core@5.0.0](https://www.npmjs.com/package/tesseract.js-core) | Apache 2.0 |
| `tesseract-core-simd.wasm` | ~3.3 MB | Tesseract engine (WebAssembly) | tesseract.js-core@5.0.0 | Apache 2.0 |
| `pdf.min.mjs` | ~420 KB | PDF.js main module | [pdfjs-dist@5.6.205](https://www.npmjs.com/package/pdfjs-dist) | Apache 2.0 |
| `pdf.worker.min.mjs` | ~1.2 MB | PDF.js rendering worker | pdfjs-dist@5.6.205 | Apache 2.0 |
| `lang/eng.traineddata.gz` | ~10 MB | Tesseract English LSTM model | [tessdata.projectnaptha.com](https://tessdata.projectnaptha.com) | Apache 2.0 |

## Why local instead of CDN?

- Works offline after the browser caches these files
- No third-party CDN uptime dependency
- No CORS surprises
- Same-origin means no MIME-type quirks with `.wasm` serving

## Updating

1. Update the npm package versions in the table above
2. Re-download matching files from unpkg:
   ```bash
   curl -o tesseract.min.js            https://unpkg.com/tesseract.js@<v>/dist/tesseract.min.js
   curl -o worker.min.js               https://unpkg.com/tesseract.js@<v>/dist/worker.min.js
   curl -o tesseract-core-simd.wasm.js https://unpkg.com/tesseract.js-core@<v>/tesseract-core-simd.wasm.js
   curl -o tesseract-core-simd.wasm    https://unpkg.com/tesseract.js-core@<v>/tesseract-core-simd.wasm
   ```
3. Keep PDF.js in sync with Folio's version (`package.json` in the `pdf-helper` repo)
