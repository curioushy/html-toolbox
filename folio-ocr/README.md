# folio-ocr — vendored dependencies

Static assets for the `folio-ocr.html` tool. All files are hosted here so the tool
works fully offline after first load (no CDN dependency).

## Contents

| File | Size | Purpose | Source | License |
|---|---|---|---|---|
| `tesseract.min.js` | ~60 KB | Tesseract.js main library | [tesseract.js@5.1.1](https://www.npmjs.com/package/tesseract.js) | Apache 2.0 |
| `worker.min.js` | ~120 KB | Tesseract.js worker script | tesseract.js@5.1.1 | Apache 2.0 |
| `tesseract-core-simd-lstm.wasm.js` | ~3.75 MB | WASM loader (SIMD + LSTM build) | [tesseract.js-core@5.1.1](https://www.npmjs.com/package/tesseract.js-core) | Apache 2.0 |
| `tesseract-core-simd-lstm.wasm` | ~2.72 MB | Tesseract SIMD engine (WebAssembly) | tesseract.js-core@5.1.1 | Apache 2.0 |
| `tesseract-core-lstm.wasm.js` | ~3.75 MB | WASM loader (non-SIMD fallback) | tesseract.js-core@5.1.1 | Apache 2.0 |
| `tesseract-core-lstm.wasm` | ~2.72 MB | Tesseract engine fallback (WebAssembly) | tesseract.js-core@5.1.1 | Apache 2.0 |
| `pdf.min.mjs` | ~420 KB | PDF.js main module | [pdfjs-dist@5.6.205](https://www.npmjs.com/package/pdfjs-dist) | Apache 2.0 |
| `pdf.worker.min.mjs` | ~1.2 MB | PDF.js rendering worker | pdfjs-dist@5.6.205 | Apache 2.0 |
| `lang/eng.traineddata.gz` | ~10 MB | Tesseract English LSTM model | [tessdata.projectnaptha.com](https://tessdata.projectnaptha.com) | Apache 2.0 |
| `pdf-lib.min.js` | ~513 KB | PDF creation / editing library | [pdf-lib@1.17.1](https://www.npmjs.com/package/pdf-lib) | MIT |

## Why local instead of CDN?

- Works offline after the browser caches these files
- No third-party CDN uptime dependency
- No CORS surprises
- Same-origin means no MIME-type quirks with `.wasm` serving

## Updating

1. Update the npm package versions in the table above
2. Re-download matching files from unpkg:
   ```bash
   curl -o tesseract.min.js                  https://unpkg.com/tesseract.js@<v>/dist/tesseract.min.js
   curl -o worker.min.js                     https://unpkg.com/tesseract.js@<v>/dist/worker.min.js
   curl -o tesseract-core-simd-lstm.wasm.js  https://unpkg.com/tesseract.js-core@<v>/tesseract-core-simd-lstm.wasm.js
   curl -o tesseract-core-simd-lstm.wasm     https://unpkg.com/tesseract.js-core@<v>/tesseract-core-simd-lstm.wasm
   curl -o tesseract-core-lstm.wasm.js       https://unpkg.com/tesseract.js-core@<v>/tesseract-core-lstm.wasm.js
   curl -o tesseract-core-lstm.wasm          https://unpkg.com/tesseract.js-core@<v>/tesseract-core-lstm.wasm
   ```
3. Keep PDF.js in sync with Folio's version (`package.json` in the `pdf-helper` repo)
