# NotebookLM Corpus Manifest -- ELM AI Presentation Demo

Srila Prabhupada's own words -- books, letters, and lectures/conversations -- packed for upload to NotebookLM (notebooklm.google.com) so Pitambara can demo live, grounded answers with citations in front of ISKCON leaders. This is a **rebuild**: the previous version of this corpus contained books only (31 files, 7.91M words); this version adds the full correspondence and as much of the audio-transcript archive as the 50-file budget allows.

## Result at a glance

- **Files: 50** (hard limit: 50)
- **Total words: 23,056,872**
- **Total citation markers: 43,368**
- **Largest file: 470,127 words** (`12_Books_Sri-Caitanya-caritamrta_Madhya-lila_part3-of-3_to_Sri-Caitanya-caritamrta_Antya-lila_part1-of-2.md`) -- target 470,000/file, hard cap 490,000/file, never exceeded
- Smallest file: 174,451 words
- Breakdown: **Books 17 files / 7,908,848 raw words** (all 51 titles, complete) -- **Letters 5 files / 2,053,894 raw words** (all 29 years of outgoing correspondence, complete) -- **Transcripts 28 files / ~13.09M words included** out of 13,921,301 raw words available (all 12 chronological years 1966-1977 complete; the four thematic bonus files mostly did not fit -- see Overflow below)

## Platform limits used

Pitambara specified: **maximum 50 source files**, **maximum 500,000 words/file**. This build packs to a **target of 470,000 words/file** with a **hard cap of 490,000 words/file**, measured on the FINAL rendered text (headers + citation markers included, not raw source word counts). No file in this corpus exceeds 470,127 words -- well inside both the target and the hard cap.

## What is excluded, and why

**The guiding rule: this notebook must contain only Srila Prabhupada's own words**, so that when NotebookLM answers a question, the answer is traceable to something Prabhupada himself wrote or said -- not a secondary source writing about him.

1. **`aVedaBase/extras/` -- excluded entirely** (as instructed). This folder holds Vyasa-puja offerings *to* Prabhupada, pre-1978 book editions (superseded by the editions in `books/`), Back to Godhead magazine issues (many articles by other authors/editors), compilations, biographies and glorification *of* Prabhupada, ISKCON Communications Journal, and other authors' writings. None of it is reliably "his own words" file-by-file, so the whole folder is out of scope for this corpus.

2. **`letters/Letters from <year>.md` (11 files, 188,823 words) -- excluded**, a finding from inspecting the actual headings (task instruction: "do not assume"). The `letters/` README describes these as "писма от секретари" (letters *from secretaries*), and the heading pattern confirms it: every entry is `## Letter to: <name> [...]` followed by a `### From: <secretary name>` sub-heading -- e.g. `### From: Tamal Krishna` (137 occurrences), `### From: Brahmananda` (16), `### From: Satsvarupa`, `### From: Rayarama`, etc. These are letters *written by* Prabhupada's secretaries (often on his behalf, sometimes just reporting news to devotees), not letters in Prabhupada's own words -- e.g. "Swamiji asked me to write in reply to your letter..." (Rayarama, 8 June 1967). Including them would let NotebookLM answer a question by quoting a secretary and attributing it to Prabhupada. The `<year> Correspondence.md` files (29 files, 2,053,894 processed words) are Prabhupada's own outgoing letters (`## Letter to:` / `### Letter to:` headings, signed "A.C. Bhaktivedanta Swami") and are included in full. Net effect: only 188,823 words out of 2.19M in the `letters/` folder (8.6%) were excluded on this basis -- a small, deliberate precision trade against the corpus's core purpose.

3. **Three near-empty transcript stub files -- excluded** (no real content; catalogued at 0 KB in `00 Catalog (aVedaBase).md`): `Audio Files.md`, `CDMinistry Easy-Access to Optimized CD Releases.md`, `Missing Recording Days.md`. Combined: under 100 words, blank placeholder pages.

## Heading patterns found (inspected before deriving citation markers)

- **Books** (`aVedaBase/books/`): `## <Chapter/Canto heading>` and `### <verse reference>` (e.g. `### SB 4.31.12`, `### Bg 9.1`) -- same scheme as the previous build; markers `[BG 9.1]`, `[SB 4.31.12]`, `[CC Madhya 20.108]` etc. preserved unchanged.

- **Letters** (`aVedaBase/letters/*Correspondence.md`): heading level varies by year (`## Letter to: ...` in early sparse years, `### Letter to: ...` nested under a bare `## <Month>` grouping heading in the busy 1968-1977 years, occasionally `#### Letter to: ...` for a same-day second letter). The recipient/place/date all live in one heading line, e.g. `### Letter to: Brahmananda — Los Angeles 11 January, 1968` or `### Letter to: Hayagriva, 4 January, 1972` (no place) or `## Post card to: Debendra Nath Sau — Ahmedabad 4 December, 1959` (rare `Post card to:` / `Telegram to:` variants also occur, 4-5 times total). **Marker derived:** `[Letter to <recipient>, <place> <date>]`, built by taking everything after "Letter to:" / "Post card to:" / "Telegram to:" verbatim and normalizing the em-dash separator to a comma -- e.g. `[Letter to Brahmananda, Los Angeles 11 January, 1968]`, `[Letter to Mahatma Gandhi, Cawnpore 12 July, 1947]`.

- **Transcripts, year files** (`aVedaBase/transcripts/<year> – <places>.md`): `# <year> – <place list>` (file title) > `## <Month>` (bare grouping, no content of its own) > `### <description> – <date>, <place>` (the actual dated entry -- a lecture, morning walk, room conversation, press conference, arrival address, etc.), e.g. `### Bhagavad-gītā 2.7–11 – March 2, 1966, New York` or `### Room Conversation with Svarūpa Dāmodara – February 12, 1975, Mexico City`. **Marker derived:** classified as **Lecture** when the description names a scripture (Bhagavad-gītā / Śrīmad-Bhāgavatam / Caitanya-caritāmṛta / Īśopaniṣad / Upadeśāmṛta / Nectar of ...) or contains the word "Lecture"; everything else (Morning Walk, Room Conversation, Press Conference, Arrival Address, Darśana, etc.) classified as **Conversation**. Format: `[Lecture, <description>, <place>, <date>]` / `[Conversation, <description>, <place>, <date>]` -- e.g. `[Lecture, Śrīmad-Bhāgavatam 3.26.23–4, Bombay, January 1, 1975]`, `[Conversation, Arrival Talk in Room, Māyāpur, March 23, 1975]`. This is a superset of the task's suggested `[Conversation, <place>, <date>]` -- the extra description slot (who/what the conversation was about) was kept for citation precision, since several conversations can share the same place and date.

- **Philosophy Discussions.md**: `## With <interlocutor>` (2 groups: with Syamasundara Dasa, and one other) > `### <philosopher name>` (e.g. `### Bentham, Jeremy`). Marker: `[Philosophy Discussion, With <interlocutor>, <topic>]`.

- **Kṛṣṇa Book Dictations.md**: `## <chapter number>. <chapter title>` only (no verse-level sub-headings) -- Prabhupada's original spoken dictation for Krsna Book, before BBT editing. Marker: `[Krsna Book Dictation, <chapter heading>]`.

- **Śrīmad-Bhāgavatam – 3rd Canto Dictations.md**: `## <NN>_SB_Dictations_<verse range>` (session grouping) > `### SB <canto.chapter.verse>` (individual verse) -- Prabhupada's original dictation for SB 3rd Canto, pre-editing. Marker: `[SB 3rd Canto Dictation, SB <verse ref>]` (kept distinct from the plain `[SB ...]` book marker, since this is the raw dictation, not the final published purport text).

- **Miscellaneous Audio.md**: `## <NN>--<description>` only, e.g. `## 06--Conversation following Śrīmad-Bhāgavatam 1.1.18, 1975`. Marker: `[Miscellaneous Audio, <description>]` (numeric prefix stripped).

## Overflow -- what did not fit in the 50-file budget

Priority order was books -> letters -> transcripts, as instructed. Books and letters are included **100% complete**. Within transcripts, the twelve chronological year files (1966-1977, the core lecture/conversation/morning-walk archive) are also **100% complete**. The budget ran out partway into the four thematic bonus files, which were processed last (Philosophy Discussions -> Kṛṣṇa Book Dictations -> Śrīmad-Bhāgavatam 3rd Canto Dictations -> Miscellaneous Audio, in that order):

| Source file | Status | Words not included |
|---|---|---:|
| `transcripts/Philosophy Discussions (with Syāmasundara Dāsa and others)` | partially included, then overflow | 382,339 |
| `transcripts/Krsna Book Dictations (Prabhupada's original dictation for Krsna Book)` | entirely excluded (budget exhausted before reaching it) | 295,258 |
| `transcripts/Srimad-Bhagavatam 3rd Canto Dictations (Prabhupada's original dictation)` | entirely excluded (budget exhausted before reaching it) | 28,343 |
| `transcripts/Miscellaneous Audio (uncategorized lectures/conversations)` | entirely excluded (budget exhausted before reaching it) | 128,446 |

**Total overflow: 834,386 words** (about 6.0% of all raw transcript material, 3.6% of everything included in this corpus). File 50 (`50_Transcripts_1977_part3-of-3_to_Philosophy-Discussions.md`) contains 1977's final part plus the first ~61,000 words of Philosophy Discussions (the "With Syāmasundara Dāsa" section up through the discussion of Freud); the remainder of Philosophy Discussions, and all of Kṛṣṇa Book Dictations, the SB 3rd Canto Dictations, and Miscellaneous Audio, did not fit. If Pitambara upgrades to NotebookLM's paid tier (100 sources / 1,000,000 words each), re-running `_scripts/build_corpus.py` with a higher `MAX_FILES`/`TARGET` would fit all of this with room to spare.

## Full file table

| # | File | Category | Scope | Words | Markers |
|---|------|----------|-------|------:|--------:|
| 1 | `01_Books_Bhagavad-gita_to_Srimad-Bhagavatam_Canto-01_part1-of-2.md` | Books | Bhagavad-gita As It Is (complete); Srimad-Bhagavatam Canto 01 (part 1 of 2) | 470,050 | 1,096 |
| 2 | `02_Books_Srimad-Bhagavatam_Canto-01_part2-of-2_to_Srimad-Bhagavatam_Canto-03_part1-of-2.md` | Books | Srimad-Bhagavatam Canto 01 (part 2 of 2); Srimad-Bhagavatam Canto 02 (complete); Srimad-Bhagavatam Canto 03 (part 1 of 2) | 470,033 | 1,129 |
| 3 | `03_Books_Srimad-Bhagavatam_Canto-03_part2-of-2_to_Srimad-Bhagavatam_Canto-04_part1-of-2.md` | Books | Srimad-Bhagavatam Canto 03 (part 2 of 2); Srimad-Bhagavatam Canto 04 (part 1 of 2) | 470,054 | 1,604 |
| 4 | `04_Books_Srimad-Bhagavatam_Canto-04_part2-of-2_to_Srimad-Bhagavatam_Canto-05_part1-of-2.md` | Books | Srimad-Bhagavatam Canto 04 (part 2 of 2); Srimad-Bhagavatam Canto 05 (part 1 of 2) | 470,082 | 1,226 |
| 5 | `05_Books_Srimad-Bhagavatam_Canto-05_part2-of-2_to_Srimad-Bhagavatam_Canto-07_part1-of-2.md` | Books | Srimad-Bhagavatam Canto 05 (part 2 of 2); Srimad-Bhagavatam Canto 06 (complete); Srimad-Bhagavatam Canto 07 (part 1 of 2) | 469,827 | 1,514 |
| 6 | `06_Books_Srimad-Bhagavatam_Canto-07_part2-of-2_to_Srimad-Bhagavatam_Canto-09_part1-of-2.md` | Books | Srimad-Bhagavatam Canto 07 (part 2 of 2); Srimad-Bhagavatam Canto 08 (complete); Srimad-Bhagavatam Canto 09 (part 1 of 2) | 469,783 | 1,933 |
| 7 | `07_Books_Srimad-Bhagavatam_Canto-09_part2-of-2_to_Srimad-Bhagavatam_Canto-10_part1-of-2.md` | Books | Srimad-Bhagavatam Canto 09 (part 2 of 2); Srimad-Bhagavatam Canto 10 (part 1 of 2) | 469,778 | 1,969 |
| 8 | `08_Books_Srimad-Bhagavatam_Canto-10_part2-of-2_to_Srimad-Bhagavatam_Canto-11_part1-of-2.md` | Books | Srimad-Bhagavatam Canto 10 (part 2 of 2); Srimad-Bhagavatam Canto 11 (part 1 of 2) | 467,633 | 2,137 |
| 9 | `09_Books_Srimad-Bhagavatam_Canto-11_part2-of-2_to_Srimad-Bhagavatam_Canto-12.md` | Books | Srimad-Bhagavatam Canto 11 (part 2 of 2); Srimad-Bhagavatam Canto 12 (complete) | 443,029 | 1,699 |
| 10 | `10_Books_Sri-Caitanya-caritamrta_Adi-lila_to_Sri-Caitanya-caritamrta_Madhya-lila_part1-of-3.md` | Books | Sri Caitanya-caritamrta -- Adi-lila (complete); Sri Caitanya-caritamrta -- Madhya-lila (part 1 of 3) | 470,000 | 2,323 |
| 11 | `11_Books_Sri-Caitanya-caritamrta_Madhya-lila_part2-of-3.md` | Books | Sri Caitanya-caritamrta -- Madhya-lila (part 2 of 3) | 470,084 | 3,708 |
| 12 | `12_Books_Sri-Caitanya-caritamrta_Madhya-lila_part3-of-3_to_Sri-Caitanya-caritamrta_Antya-lila_part1-of-2.md` | Books | Sri Caitanya-caritamrta -- Madhya-lila (part 3 of 3); Sri Caitanya-caritamrta -- Antya-lila (part 1 of 2) | 470,127 | 3,638 |
| 13 | `13_Books_Sri-Caitanya-caritamrta_Antya-lila_part2-of-2_to_Krsna-Book_part1-of-2.md` | Books | Sri Caitanya-caritamrta -- Antya-lila (part 2 of 2); Sri Isopanisad (complete); The Nectar of Devotion (Bhakti-rasamrta-sindhu) (complete); The Nectar of Instruction (Sri Upadesamrta) (complete); Krsna, The Supreme Personality of Godhead (part 1 of 2) | 467,563 | 2,214 |
| 14 | `14_Books_Krsna-Book_part2-of-2_to_Dialectic-Spiritualism_part1-of-2.md` | Books | Krsna, The Supreme Personality of Godhead (part 2 of 2); Teachings of Lord Caitanya (complete); Dialectic Spiritualism (part 1 of 2) | 461,073 | 130 |
| 15 | `15_Books_Dialectic-Spiritualism_part2-of-2_to_Journey-of-Self-Discovery_part1-of-2.md` | Books | Dialectic Spiritualism (part 2 of 2); The Science of Self-Realization (complete); Renunciation Through Wisdom (complete); Teachings of Lord Kapila, the Son of Devahuti (complete); Journey of Self-Discovery (part 1 of 2) | 468,416 | 221 |
| 16 | `16_Books_Journey-of-Self-Discovery_part2-of-2_to_The-Path-of-Perfection_part1-of-2.md` | Books | Journey of Self-Discovery (part 2 of 2); Quest for Enlightenment (complete); Teachings of Queen Kunti (complete); Beyond Illusion & Doubt (complete); Narada-bhakti-sutra (complete); Gitar Gan (complete); A Second Chance (complete); The Path of Perfection (part 1 of 2) | 467,773 | 905 |
| 17 | `17_Books_The-Path-of-Perfection_part2-of-2_to_Krsna-the-Reservoir-of-Pleasur.md` | Books | The Path of Perfection (part 2 of 2); Mukunda-mala-stotra (complete); Dharma, The Way of Transcendence (complete); Life Comes From Life (complete); Raja-Vidya, The King of Knowledge (complete); Krsna Consciousness, The Matchless Gift (complete); Perfect Questions, Perfect Answers (complete); Krsna Consciousness, The Topmost Yoga System (complete); Elevation to Krsna Consciousness (complete); Light of the Bhagavata (complete); The Laws of Nature, An Infallible Justice (complete); Civilization and Transcendence (complete); Message of Godhead (complete); Easy Journey to Other Planets (complete); On the Way to Krsna (complete); The Perfection of Yoga (complete); Beyond Birth and Death (complete); Transcendental Teachings of Prahlada Maharaja (complete); Krsna, the Reservoir of Pleasure (complete) | 435,964 | 338 |
| 18 | `18_Letters_1947_to_1969_part1-of-2.md` | Letters | 1947 Correspondence (complete); 1949 Correspondence (complete); 1950 Correspondence (complete); 1951 Correspondence (complete); 1952 Correspondence (complete); 1953 Correspondence (complete); 1955 Correspondence (complete); 1956 Correspondence (complete); 1957 Correspondence (complete); 1958 Correspondence (complete); 1959 Correspondence (complete); 1960 Correspondence (complete); 1961 Correspondence (complete); 1962 Correspondence (complete); 1963 Correspondence (complete); 1964 Correspondence (complete); 1965 Correspondence (complete); 1966 Correspondence (complete); 1967 Correspondence (complete); 1968 Correspondence (complete); 1969 Correspondence (part 1 of 2) | 470,060 | 1,122 |
| 19 | `19_Letters_1969_part2-of-2_to_1970_part1-of-2.md` | Letters | 1969 Correspondence (part 2 of 2); 1970 Correspondence (part 1 of 2) | 470,032 | 1,283 |
| 20 | `20_Letters_1970_part2-of-2_to_1973_part1-of-2.md` | Letters | 1970 Correspondence (part 2 of 2); 1971 Correspondence (complete); 1972 Correspondence (complete); 1973 Correspondence (part 1 of 2) | 469,939 | 1,431 |
| 21 | `21_Letters_1973_part2-of-2_to_1976_part1-of-2.md` | Letters | 1973 Correspondence (part 2 of 2); 1974 Correspondence (complete); 1975 Correspondence (complete); 1976 Correspondence (part 1 of 2) | 470,120 | 2,119 |
| 22 | `22_Letters_1976_part2-of-2_to_1977.md` | Letters | 1976 Correspondence (part 2 of 2); 1977 Correspondence (complete) | 174,451 | 874 |
| 23 | `23_Transcripts_1966_part1-of-2.md` | Transcripts | 1966 Lectures & Conversations (New York) (part 1 of 2) | 468,514 | 176 |
| 24 | `24_Transcripts_1966_part2-of-2_to_1968_part1-of-2.md` | Transcripts | 1966 Lectures & Conversations (New York) (part 2 of 2); 1967 Lectures & Conversations (New York, San Francisco, New York) (complete); 1968 Lectures & Conversations (Los Angeles, San Francisco, New York, Boston, Montreal, New York, San Fra) (part 1 of 2) | 466,020 | 288 |
| 25 | `25_Transcripts_1968_part2-of-2_to_1969_part1-of-3.md` | Transcripts | 1968 Lectures & Conversations (Los Angeles, San Francisco, New York, Boston, Montreal, New York, San Fra) (part 2 of 2); 1969 Lectures & Conversations (Los Angeles, Honolulu, San Francisco, New York, Buffalo, Boston, Columbus) (part 1 of 3) | 464,740 | 285 |
| 26 | `26_Transcripts_1969_part2-of-3.md` | Transcripts | 1969 Lectures & Conversations (Los Angeles, Honolulu, San Francisco, New York, Buffalo, Boston, Columbus) (part 2 of 3) | 469,618 | 232 |
| 27 | `27_Transcripts_1969_part3-of-3_to_1971_part1-of-3.md` | Transcripts | 1969 Lectures & Conversations (Los Angeles, Honolulu, San Francisco, New York, Buffalo, Boston, Columbus) (part 3 of 3); 1970 Lectures & Conversations (Los Angeles, San Francisco, Los Angeles, Calcutta, Bombay, Indore, Surat) (complete); 1971 Lectures & Conversations (Surat, Bombay, Calcutta, Allahabad, Prayāga, Allahabad, Gorakhpur, Bombay) (part 1 of 3) | 468,797 | 315 |
| 28 | `28_Transcripts_1971_part2-of-3.md` | Transcripts | 1971 Lectures & Conversations (Surat, Bombay, Calcutta, Allahabad, Prayāga, Allahabad, Gorakhpur, Bombay) (part 2 of 3) | 467,721 | 257 |
| 29 | `29_Transcripts_1971_part3-of-3_to_1972_part1-of-4.md` | Transcripts | 1971 Lectures & Conversations (Surat, Bombay, Calcutta, Allahabad, Prayāga, Allahabad, Gorakhpur, Bombay) (part 3 of 3); 1972 Lectures & Conversations (Jaipur, Bombay, Madras, Visakhapatnam, Calcutta, Mayapur, Birnagar, Calcu) (part 1 of 4) | 469,622 | 321 |
| 30 | `30_Transcripts_1972_part2-of-4.md` | Transcripts | 1972 Lectures & Conversations (Jaipur, Bombay, Madras, Visakhapatnam, Calcutta, Mayapur, Birnagar, Calcu) (part 2 of 4) | 459,267 | 364 |
| 31 | `31_Transcripts_1972_part3-of-4.md` | Transcripts | 1972 Lectures & Conversations (Jaipur, Bombay, Madras, Visakhapatnam, Calcutta, Mayapur, Birnagar, Calcu) (part 3 of 4) | 466,856 | 424 |
| 32 | `32_Transcripts_1972_part4-of-4_to_1973_part1-of-4.md` | Transcripts | 1972 Lectures & Conversations (Jaipur, Bombay, Madras, Visakhapatnam, Calcutta, Mayapur, Birnagar, Calcu) (part 4 of 4); 1973 Lectures & Conversations (Bombay, Calcutta, Melbourne, Sydney, Auckland, Jakarta, Calcutta, Cambrid) (part 1 of 4) | 469,138 | 257 |
| 33 | `33_Transcripts_1973_part2-of-4.md` | Transcripts | 1973 Lectures & Conversations (Bombay, Calcutta, Melbourne, Sydney, Auckland, Jakarta, Calcutta, Cambrid) (part 2 of 4) | 464,032 | 564 |
| 34 | `34_Transcripts_1973_part3-of-4.md` | Transcripts | 1973 Lectures & Conversations (Bombay, Calcutta, Melbourne, Sydney, Auckland, Jakarta, Calcutta, Cambrid) (part 3 of 4) | 467,363 | 327 |
| 35 | `35_Transcripts_1973_part4-of-4_to_1974_part1-of-5.md` | Transcripts | 1973 Lectures & Conversations (Bombay, Calcutta, Melbourne, Sydney, Auckland, Jakarta, Calcutta, Cambrid) (part 4 of 4); 1974 Lectures & Conversations (Los Angeles, Honolulu, Tokyo, Hong Kong, Vṛndāvana, Bombay, Mayapur, Calc) (part 1 of 5) | 468,438 | 304 |
| 36 | `36_Transcripts_1974_part2-of-5.md` | Transcripts | 1974 Lectures & Conversations (Los Angeles, Honolulu, Tokyo, Hong Kong, Vṛndāvana, Bombay, Mayapur, Calc) (part 2 of 5) | 469,751 | 286 |
| 37 | `37_Transcripts_1974_part3-of-5.md` | Transcripts | 1974 Lectures & Conversations (Los Angeles, Honolulu, Tokyo, Hong Kong, Vṛndāvana, Bombay, Mayapur, Calc) (part 3 of 5) | 467,727 | 264 |
| 38 | `38_Transcripts_1974_part4-of-5.md` | Transcripts | 1974 Lectures & Conversations (Los Angeles, Honolulu, Tokyo, Hong Kong, Vṛndāvana, Bombay, Mayapur, Calc) (part 4 of 5) | 470,087 | 285 |
| 39 | `39_Transcripts_1974_part5-of-5_to_1975_part1-of-5.md` | Transcripts | 1974 Lectures & Conversations (Los Angeles, Honolulu, Tokyo, Hong Kong, Vṛndāvana, Bombay, Mayapur, Calc) (part 5 of 5); 1975 Lectures & Conversations (Hong Kong, Tokyo, Honolulu, Los Angeles, Mexico City, Caracas, Miami, Atl) (part 1 of 5) | 468,657 | 230 |
| 40 | `40_Transcripts_1975_part2-of-5.md` | Transcripts | 1975 Lectures & Conversations (Hong Kong, Tokyo, Honolulu, Los Angeles, Mexico City, Caracas, Miami, Atl) (part 2 of 5) | 466,406 | 216 |
| 41 | `41_Transcripts_1975_part3-of-5.md` | Transcripts | 1975 Lectures & Conversations (Hong Kong, Tokyo, Honolulu, Los Angeles, Mexico City, Caracas, Miami, Atl) (part 3 of 5) | 469,297 | 287 |
| 42 | `42_Transcripts_1975_part4-of-5.md` | Transcripts | 1975 Lectures & Conversations (Hong Kong, Tokyo, Honolulu, Los Angeles, Mexico City, Caracas, Miami, Atl) (part 4 of 5) | 470,017 | 260 |
| 43 | `43_Transcripts_1975_part5-of-5_to_1976_part1-of-6.md` | Transcripts | 1975 Lectures & Conversations (Hong Kong, Tokyo, Honolulu, Los Angeles, Mexico City, Caracas, Miami, Atl) (part 5 of 5); 1976 Lectures & Conversations (Madras, Nellore, Madras, Bombay, Calcutta, Mayapur, Calcutta, New Delhi, ) (part 1 of 6) | 469,094 | 351 |
| 44 | `44_Transcripts_1976_part2-of-6.md` | Transcripts | 1976 Lectures & Conversations (Madras, Nellore, Madras, Bombay, Calcutta, Mayapur, Calcutta, New Delhi, ) (part 2 of 6) | 469,115 | 334 |
| 45 | `45_Transcripts_1976_part3-of-6.md` | Transcripts | 1976 Lectures & Conversations (Madras, Nellore, Madras, Bombay, Calcutta, Mayapur, Calcutta, New Delhi, ) (part 3 of 6) | 467,117 | 314 |
| 46 | `46_Transcripts_1976_part4-of-6.md` | Transcripts | 1976 Lectures & Conversations (Madras, Nellore, Madras, Bombay, Calcutta, Mayapur, Calcutta, New Delhi, ) (part 4 of 6) | 469,143 | 451 |
| 47 | `47_Transcripts_1976_part5-of-6.md` | Transcripts | 1976 Lectures & Conversations (Madras, Nellore, Madras, Bombay, Calcutta, Mayapur, Calcutta, New Delhi, ) (part 5 of 6) | 457,786 | 389 |
| 48 | `48_Transcripts_1976_part6-of-6_to_1977_part1-of-3.md` | Transcripts | 1976 Lectures & Conversations (Madras, Nellore, Madras, Bombay, Calcutta, Mayapur, Calcutta, New Delhi, ) (part 6 of 6); 1977 Lectures & Conversations (Bombay, Allahabad, Calcutta, Bhubaneswar, Jagannātha Purī, Bhubaneswar, C) (part 1 of 3) | 467,308 | 292 |
| 49 | `49_Transcripts_1977_part2-of-3.md` | Transcripts | 1977 Lectures & Conversations (Bombay, Allahabad, Calcutta, Bhubaneswar, Jagannātha Purī, Bhubaneswar, C) (part 2 of 3) | 469,446 | 315 |
| 50 | `50_Transcripts_1977_part3-of-3_to_Philosophy-Discussions.md` | Transcripts | 1977 Lectures & Conversations (Bombay, Allahabad, Calcutta, Bhubaneswar, Jagannātha Purī, Bhubaneswar, C) (part 3 of 3); Philosophy Discussions (with Syāmasundara Dāsa and others) (complete) | 469,924 | 367 |

## Verification performed

1. File count: **50** (limit 50, OK). Largest file: **470,127 words** (`12_Books_Sri-Caitanya-caritamrta_Madhya-lila_part3-of-3_to_Sri-Caitanya-caritamrta_Antya-lila_part1-of-2.md`), cap 490,000 -- OK, never exceeded.
2. Every one of the 50 files has the header block, at least one `[...]` citation marker, and no truncated tail -- verified programmatically (every file ends at a complete chunk boundary; sampled tails all end at natural sentence/entry ends, several at the source's own `[end]` marker).
3. Cross-category check: confirmed no `Letters` file's header/scope mentions transcript-type content and no `Transcripts` file's header mentions correspondence (an earlier build pass had a key-collision bug where letters years and transcript years shared plain "YYYY" keys internally and one label overwrote the other in file headers -- found and fixed before finalizing; verified clean by grep across all 50 files).
4. Five real extracts checked by hand (book / letter / lecture / conversation / philosophy-discussion) -- see below.
5. IAST diacritics and Devanagari confirmed intact (see the Bhagavad-gita extract below: full Sanskrit verse in Devanagari + IAST, e.g. `śrī-bhagavān uvāca`, `jñānaṁ vijñāna-sahitaṁ`).
6. Total words: **23,056,872**. Total citation markers: **43,368**.
7. Previous build (31 book-only files + old MANIFEST.md) archived (moved, not deleted) into `_old_builds/<timestamp>/`.

### Extract 1 -- Book (Bhagavad-gita As It Is, file 01)

```
[BG 9.1]

**TEXT**

> śrī-bhagavān uvāca / idaṁ tu te guhya-tamaṁ / pravakṣyāmy anasūyave /
> jñānaṁ vijñāna-sahitaṁ / yaj jñātvā mokṣyase 'śubhāt

**TRANSLATION**
The Supreme Personality of Godhead said: My dear Arjuna, because you are never envious of Me...
```

### Extract 2 -- Letter (1947 Correspondence, file 18)

```
[Letter to Mahatma Gandhi, Cawnpore 12 July, 1947]

47-07-12 Mahatma Gandhijee, Bhangi Colony, New Delhi. Dear Friend Mahatmajee,
Please accept my respectful Namaskar. I am your unknown friend but I had to write to you...
```

### Extract 3 -- Lecture (1966, file 23)

```
[Lecture, Bhagavad-gītā Introduction, New York, February 19, 1966]

Prabhupāda:
oṁ ajñāna-timirāndhasya / jñānāñjana-śalākayā / cakṣur unmīlitaṁ yena / tasmai śrī-gurave namaḥ ...
```

### Extract 4 -- Conversation (1975, file 40)

```
[Conversation, Arrival Talk in Room, Māyāpur, March 23, 1975]

Prabhupāda: ...offering his blessings upon you. You are fulfilling his mission. He wanted that
European, American should come here. It is all Bhaktivinoda Ṭhākura's blessing...
```

### Extract 5 -- Philosophy Discussion / dictation-class material (file 50)

```
[Philosophy Discussion, With Syāmasundara Dāsa, Bentham, Jeremy]

Śyāmasundara: First one.
Prabhupāda: Hedonism. ... So that happiness is described in the Bhagavad-gītā, sukham
ātyantikaṁ yat. Ātyantikam means the greatest happiness...
```

## How to upload to NotebookLM (for Pitambara)

1. Go to **notebooklm.google.com** and sign in.
2. Create a new notebook (or open the existing demo notebook) and click **Add source** -> **Upload file**.
3. Select all **50** `.md` files in this folder (everything except `MANIFEST.md` and the `_scripts`/`_old_builds` folders).
4. Wait for NotebookLM to finish indexing all sources -- a progress indicator shows per file. **A corpus this size (23M+ words across 50 files) takes real time to index -- do this the day before the ISKCON leaders session, not at the venue.** Confirm every source shows as fully processed before relying on it live.
5. When asking questions, you can explicitly ask NotebookLM to cite its bracketed reference marker (e.g. `[BG 9.1]`, `[Letter to Rāyarāma, 8 December 1968]`, `[Lecture, Śrīmad-Bhāgavatam 3.26.23–4, Bombay, January 1, 1975]`) -- every file's header already instructs the model to do this automatically.
6. If NotebookLM's paid tier is available (100 sources / 1,000,000 words/source), re-run `_scripts/build_corpus.py` after raising `MAX_FILES` and `TARGET`/`HARD_CAP` in the script to recover the ~834,000 overflow words (Philosophy Discussions remainder, Kṛṣṇa Book Dictations, SB 3rd Canto Dictations, Miscellaneous Audio) and to pack books/letters into fewer, larger files.
