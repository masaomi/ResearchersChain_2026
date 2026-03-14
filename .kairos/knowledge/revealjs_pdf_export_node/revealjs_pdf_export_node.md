---
name: revealjs_pdf_export_node
description: Convert Reveal.js HTML slides to PDF using Node.js + Puppeteer (local file workflow)
version: 1.0
tags: [revealjs, pdf, nodejs, puppeteer, presentation, workflow]
---

# Reveal.js to PDF (Node/Puppeteer)

Use this workflow to export a local Reveal.js HTML presentation to PDF.

## Prerequisites

- `puppeteer` installed in the project (`package.json` dependency)
- Chrome for Puppeteer installed once:

```bash
npx puppeteer browsers install chrome
```

## Export command

Run from repository root and adjust paths as needed.

```bash
node --input-type=module -e "import puppeteer from 'puppeteer'; import path from 'path'; const htmlPath = path.resolve('final_report_20260306/presentation/lab_meeting_20260309_v3.html'); const pdfPath = path.resolve('final_report_20260306/presentation/lab_meeting_20260309_v3.pdf'); const browser = await puppeteer.launch({headless:true, args:['--no-sandbox','--disable-setuid-sandbox']}); const page = await browser.newPage(); await page.goto('file://' + htmlPath + '?print-pdf', {waitUntil:'networkidle0'}); await page.emulateMediaType('print'); await page.pdf({path: pdfPath, printBackground: true, preferCSSPageSize: true, margin: {top:'0', right:'0', bottom:'0', left:'0'}}); await browser.close(); console.log('PDF saved to ' + pdfPath);"
```

## Notes

- Keep `?print-pdf` in the URL for Reveal.js print layout.
- Use `printBackground: true` so colored boxes and backgrounds are preserved.
- Use `preferCSSPageSize: true` to follow Reveal.js/CSS page settings.
- The `--no-sandbox` flags may be required in constrained environments.
- Re-run export after slide edits to refresh the PDF.