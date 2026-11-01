# How this repository was made (Lamongan Regency (Indonesia))

This file is written by the build on 2026-11-01, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
| JDIH Kabupaten Lamongan (Bagian Hukum Sekretariat Daerah Kabupaten Lamongan): Peraturan Daerah, each the published copy (salinan) as a PDF with a text layer | <https://jdih.lamongankab.go.id> | 2026-11-01 | Peraturan Daerah of Kabupaten Lamongan as published (salinan) on https://jdih.lamongankab.go.id. Undang-Undang Nomor 28 Tahun 2014 tentang Hak Cipta, Pasal 42: "Tidak ada Hak Cipta atas hasil karya berupa: a. hasil rapat terbuka lembaga negara; b. peraturan perundang-undangan; c. pidato kenegaraan atau pidato pejabat Pemerintah; d. putusan pengadilan atau penetapan hakim; dan e. kitab suci atau simbol keagamaan." (There is no copyright in ... b. laws and regulations.) A Peraturan Daerah Kabupaten/Kota is one of the peraturan perundang-undangan listed in Pasal 7(1) huruf g of Undang-Undang Nomor 12 Tahun 2011. |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `perda-2016-012-perubahan-atas-peraturan-daerah-nomor-18-tahun-2010-tentang-retribusi` | PERATURAN DAERAH KABUPATEN LAMONGAN NOMOR 12 TAHUN 2016 TENTANG PERUBAHAN ATAS PERATURAN DAERAH NOMOR 18 TAHUN 2010 TENTANG RETRIBUSI PEMAKAIAN KEKAYAAN DAERAH | 1 | 2016-12-05 to 2016-12-05 |

The build made 1 commits:

| Commits | Kind |
| ---: | --- |
| 1 | first version of an act |
| 0 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-11-01.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 1 laws in the record.
- 1 tags.

## Dates

Each commit is dated at noon (Asia/Jakarta) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: A Peraturan Daerah takes effect on the day its last Pasal names; almost always "mulai berlaku pada tanggal diundangkan", the day it is promulgated in the Lembaran Daerah. https://jdih.lamongankab.go.id

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `876f25900dab381b6bd2763de01684a638267a0f5c58931a01497ef3c8a46dd8` (15509 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3d00541d258745461ab52b1b0cb4e1716a27a95d`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.12.10; git version 2.46.0.windows.1.

## Checks

1 versions of 1 acts read back from git on the day each took effect and on the day before: 0 mismatches. Trailers: 0 commits whose trailers git cannot parse. Health: 0 merge commits on main, 0 commit dates that go backwards, 0 commits dated after the build.

No second build of this corpus has been compared yet.

## Decisions made by hand

- Oldest version available: each Peraturan Daerah is one version, its text as enacted (the published copy, salinan), credited to the JDIH publisher (first_law null), not to an amending law. An amending Perda is recorded as an act of its own; its changes are not replayed into the Perda it amends, and a repeal is not applied.
- Dated by the day the Perda takes effect under its own last Pasal: the promulgation day (diundangkan, printed in the closing) when it says "mulai berlaku pada tanggal diundangkan", or the calendar day it names. A Perda whose commencement is a period or another event is left out for now.
- Parts are added oldest first, so each part only adds history after the last one.
- Units: a-pembukaan (heading, preamble, enacting words), one file per Pasal (chapter, part and paragraph headings printed between two Pasal stay at the end of the earlier one, in printed order), z1-penutup (promulgation order, signatures, Lembaran Daerah number, certification), z2-penjelasan (the elucidation) and z3-lampiran (the annex) where printed. One paragraph per line.
- Left out of the text: page numbers and the "SALINAN" stamp line. Text-layer PDFs only (no OCR): scans are left out.
- Every Perda is checked by a second PDF reader (pdftotext): each paragraph of the record, letters and digits only, must be one unbroken stretch of the PDF, and together they must cover the whole PDF with nothing left over except page numbers and the stamp. A Perda that fails is left out.

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code (claude-opus-5-5) wrote Lexifina's code and chose the sources. No model output is used as legal text or dates: every word comes from the PDFs published on JDIH.
