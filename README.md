# IL-SUNG TECH · OQC Quality Dashboard

Static report based on **October 1–30, 2026** Excel data. Data and charts are bundled into `index.html`. No ERP or Sheets API is used in this version.

## Open the dashboard

- GitHub Pages (after **Custom domain** is removed until DNS is ready): https://ilsungdata-wq.github.io/oqc-dashboard/
- Download `index.html` and open in Chrome for local review.
- GitHub Pages currently has a custom domain configured, so the default URL may redirect until that setting is removed.

## Update November without a backend

1. Open Dashboard → **Danh mục & Target** → **Tải Excel mẫu** (or use the separately supplied `OQC_Excel_Update_Template.xlsx`).
2. Enter defect rows into sheet **OQC_ERRORS**: `Date, Line, Shift, Model, Defect, Qty, Slot, Code, Status`.
3. Enter production rows into sheet **OUTPUT**: `Date, Line, Shift, Model, Output`.
4. Dashboard → **Nhập Excel tháng khác**. Validate all KPI and time filters.
5. Click **Xuất JSON cập nhật website**, saving `current.json`.
6. In this repository, create or update **`data/current.json`** with that file, commit to `main`, and allow GitHub Pages to redeploy. The same shared link will then show the new period. Importing Excel in one browser **does not update other viewers**.
7. For shared targets, click **Xuất cấu hình Target**, then upload the resulting `targets.json` as **`data/targets.json`**.

The **Xuất Excel** control exports the currently filtered errors and output with Target sheets. It needs the SheetJS browser library, loaded on demand from `cdn.sheetjs.com`. If blocked, CSV export is provided as a fallback.

## Definitions

- OQC (%) = defect occurrences / output × 100. This is **not** necessarily unique defective EA.
- Scrap EA = sum of error Qty where Defect contains the word "Scrap" (case-insensitive).
- Scrap (%) = Scrap EA / Output × 100.
- Target rules: Model-specific target overrides product-type target; **actual > target = red**.
- October source includes slot codes A–E, not exact hour timestamps.

## Security

**This repository is public** and the embedded October quality data is accessible to anyone with the URL or source code. Obtain company authorization before distributing externally. Do not add credentials, token keys, HR data, or other restricted information to this repository.
