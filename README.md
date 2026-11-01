# Lamongan Regency (Indonesia): law history in git

The Peraturan Daerah (Perda) of Kabupaten Lamongan, Indonesia, as a git history: one folder per Perda, one file per Pasal (article), one paragraph per line, so `git blame`, `git log` and `git diff` work line by line. The text is the Indonesian text of each Perda as enacted, from the copy (salinan) published by JDIH Kabupaten Lamongan (Bagian Hukum Sekretariat Daerah Kabupaten Lamongan).

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law).

## What this repository holds

**Each Perda as enacted, not yet a history of amendments.** JDIH publishes each Perda as its signed copy; there is no consolidated text. So each Perda is one commit holding its text as enacted ("oldest version available"), credited to the publisher, not to an amending law. An amending Perda is its own folder; its amendments are not applied to the Perda it amends, and a repeal is not applied.

| File | What |
| --- | --- |
| `a-pembukaan.md` | heading, title, preamble (Menimbang, Mengingat) and enacting words |
| `pasal-NNN.md` | one Pasal; chapter, part and paragraph headings printed before the next Pasal stay at its end |
| `z1-penutup.md` | promulgation order, signatures, Lembaran Daerah number, certification of the copy |
| `z2-penjelasan.md` | the elucidation (Penjelasan), where printed |
| `z3-lampiran.md` | the annex (Lampiran), where printed |

The record is built in parts, oldest Perda first, and holds only the Perda JDIH publishes as a PDF that passes the checks below (a text layer, or a scan read by OCR); documents the reader cannot split into Pasal are left out for now. Scans are read by OCR (see "OCR texts"). Budgets (APBD and their accountability reports), development plans (RPJMD, RPJPD) and spatial plans (RTRW, zoning), which are mostly tables and maps, are not included. It is not (yet) every Perda of Kabupaten Lamongan.

## Source

[JDIH Kabupaten Lamongan (Bagian Hukum Sekretariat Daerah Kabupaten Lamongan)](https://jdih.lamongankab.go.id): each Perda as a PDF (a text layer, or a scan read by OCR). Each PDF's sha256 is recorded with its version in `data/versions.json`.

## Dates

Each Perda is dated by the day it takes effect under its own last Pasal, at noon local time (WIB, UTC+7): the day it was promulgated (diundangkan, printed in its closing) when it says "mulai berlaku pada tanggal diundangkan", or the calendar day it names. Perda whose commencement is a period after promulgation or another event are left out for now.

## How it is built

Lexifina reads the sources listed here and records each act's dated versions, and the laws that made each change, in one corpus file. `tools/build.py` writes this repository from that file, and the same corpus always gives the same commit hashes; `REPRODUCE.md` gives the details and the checks. A model (Claude) wrote Lexifina's code; it wrote no legal text, and no model runs when the history is built.

The text layer of each PDF becomes the record (scans: see "OCR texts" below), row by row in reading order, rows joined into paragraphs. Left out: page numbers and the "SALINAN" stamp line. Nothing is reworded.

## OCR texts

18 Perda in this repository are read by OCR from the official scans JDIH publishes (Alan's decision D8, 2026-11-02: OCR is allowed for official scans whose terms allow reuse, marked as OCR and spot-checked). Each such file starts with a front-matter line

    Text-source: OCR (Tesseract <version>, ind) of the official scan <url>

and its commit message says the same. Reader: Tesseract (tessdata_best model "ind", --psm 3, pages at 300 dpi); pages with a real text layer keep it; lines with no letter or digit are left out. The strict letters check needs a text layer, so these acts are spot-checked instead: 3 paragraphs of every act, drawn at random, are cut out of the scan and read again with a different setting (tessdata_fast, --psm 6); the two readings must agree at 98% or more, character for character, or the act is left out. The structural checks still apply (Pasal in order, the closing formula, the promulgation day, the number and year against JDIH). OCR can misread single characters, so for anything that matters, read the scan.

They were added after the text-layer history, at its end (D12): some are dated before acts published earlier.

| Act | In force | Spot-check agreement | Scan | Part |
| --- | --- | --- | --- | --- |
| Perda Lamongan Regency 1/2015 | 2015-03-10 | 99.75% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-1-tahun-2015-tentang-prasarana-60/download> | 30-ocr-01 |
| Perda Lamongan Regency 14/2015 | 2016-03-15 | 99.84% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-14-tahun-2015-tentang-penataan-70/download> | 30-ocr-01 |
| Perda Lamongan Regency 9/2016 | 2016-10-25 | 99.44% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-9-tahun-2016-tentang-perubahan-56/download> | 30-ocr-01 |
| Perda Lamongan Regency 7/2018 | 2018-11-26 | 100.00% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupatel-lamongan-nomor-7-tahun-2018-tentang-penyelengaraan-31/download> | 30-ocr-01 |
| Perda Lamongan Regency 10/2018 | 2018-12-10 | 99.72% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-10-tahun-2018-tentang-pencabutan-34/download> | 30-ocr-01 |
| Perda Lamongan Regency 15/2018 | 2018-12-31 | 99.63% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-15-tahun-2018-tentang-pelestarian-38/download> | 30-ocr-01 |
| Perda Lamongan Regency 8/2019 | 2019-08-09 | 100.00% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-8-tahun-2019-tentang-badan-16/download> | 30-ocr-01 |
| Perda Lamongan Regency 14/2019 | 2019-10-23 | 99.73% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-14-tahun-2019-tentang-penyelenggaraan-21/download> | 30-ocr-01 |
| Perda Lamongan Regency 19/2019 | 2019-10-23 | 99.85% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-19-tahun-2019-tentang-perubahan-2427/download> | 30-ocr-01 |
| Perda Lamongan Regency 1/2021 | 2021-02-04 | 99.77% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-1-tahun-2021-tentang-pencabutan-peraturan-daerah-no-7-tahun-2005-tentang-transparansi-penyelenggaraan-pemerintahan-dan-partisipasi-masyarakat-di-kabupaten-lamongan/download> | 30-ocr-01 |
| Perda Lamongan Regency 4/2021 | 2021-03-02 | 99.78% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-4-tahun-2021-tentang-kawasan-tanpa-rokok/download> | 30-ocr-01 |
| Perda Lamongan Regency 12/2021 | 2021-09-24 | 99.87% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-12-tahun-2021-tentang-inovasi-daerah/download> | 30-ocr-01 |
| Perda Lamongan Regency 15/2021 | 2021-11-24 | 99.55% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-15-tahun-2021-tentang-penyelenggaraan-penanggulangan-bencana-alam-dan-non-alam/download> | 30-ocr-01 |
| Perda Lamongan Regency 16/2021 | 2021-12-27 | 100.00% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-16-tahun-2021-tentang-penanggulangan-kemiskinan/download> | 30-ocr-01 |
| Perda Lamongan Regency 2/2023 | 2023-01-31 | 99.76% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-2-tahun-2023-tentang-retribusi-penggunaan-tenaga-kerja-asing/download> | 30-ocr-01 |
| Perda Lamongan Regency 6/2023 | 2023-08-01 | 100.00% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-6-tahun-2023-tentang-pencabutan-peraturan-daerah-kabupaten-lamongan-nomor-9-tahun-2011-tentang-ijin-usaha-jasa-konstruksi-di-kabupaten-lamongan/download> | 30-ocr-01 |
| Perda Lamongan Regency 2/2026 | 2026-04-16 | 100.00% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-2-tahun-2026-tentang-penataan-dan-pengendalian-infrastruktur-pasif-telekomunikasi-1/download> | 30-ocr-01 |
| Perda Lamongan Regency 4/2026 | 2026-04-23 | 98.79% | <https://jdih.lamongankab.go.id/api/documents/peraturan-daerah-kabupaten-lamongan-nomor-4-tahun-2026-tentang-perubahan-atas-peraturan-daerah-nomor-16-tahun-2019-tentang-pengendalian-dan-pengawasan-minuman-beralkohol/download> | 30-ocr-01 |

## How it is checked

Every version is read back from git on the day it took effect and must match the corpus. A second, independent reading of every PDF (a different PDF engine, pdftotext) must hold every paragraph of the record as one unbroken stretch, letter for letter and digit for digit, and the paragraphs together must cover the whole PDF with nothing left over but page numbers and the stamp. Results are in `REPRODUCE.md`.

## What "author" means

The author of each commit is the publisher, with an e-mail address that cannot exist; the committer is always Lexifina.

## Limits

Only each Perda as enacted: no later amendments, no consolidation, no repeal applied, Indonesian text only, and only the Perda that pass the checks; OCR'd texts may misread single characters. The official text is the one promulgated in the Lembaran Daerah.

## Licence

See [LICENSE](LICENSE): Undang-Undang Nomor 28 Tahun 2014 tentang Hak Cipta, Pasal 42, gives no copyright in peraturan perundang-undangan. Source: JDIH Kabupaten Lamongan (Bagian Hukum Sekretariat Daerah Kabupaten Lamongan), https://jdih.lamongankab.go.id.
