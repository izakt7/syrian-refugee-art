# Google Sheet Template - Copy This Into Your Sheet

## ⚠️ IMPORTANT: Each Item = One Column

**YES!** Each item (pid, title, artist, etc.) should be in a **separate column** in Google Sheets.

Think of it like this:
- **Row 1** = Column headers (one header per column)
- **Row 2+** = Your artwork data (one artwork per row)

**Visual Example:**
```
Google Sheet Layout:

     Column A    Column B         Column C      Column D    Column E          ...
Row 1: pid       title            artist        date        description
Row 2: artwork1  Sunset Over...   Ahmed Ali     2020        A beautiful...
Row 3: artwork2  Refugee Camp...  Samira        2019        Daily life...
```

Each column header goes in its own column, and each piece of data goes in the matching column below it.

---

## Column Headers (Row 1)

**YES - Each item goes in a SEPARATE column!**

In Google Sheets, create 11 columns. Put each header in its own column:

| Column A | Column B | Column C | Column D | Column E | Column F | Column G | Column H | Column I | Column J | Column K | Column L | Column M | Column N |
|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|
| **pid** | **title** | **artist** | **date** | **description** | **medium** | **location** | **layout** | **collection** | **thumbnail** | **full** | **manifest** | **video_url** | **audio_url** |

**Visual Guide:**
```
Column A: pid
Column B: title  
Column C: artist
Column D: date
Column E: description
Column F: medium
Column G: location
Column H: layout
Column I: collection
Column J: thumbnail
Column K: full
Column L: manifest
Column M: video_url (optional - for videos)
Column N: audio_url (optional - for audio)
```

**Quick Setup:**
1. Click on cell A1, type: `pid`
2. Click on cell B1, type: `title`
3. Click on cell C1, type: `artist`
4. Click on cell D1, type: `date`
5. Click on cell E1, type: `description`
6. Click on cell F1, type: `medium`
7. Click on cell G1, type: `location`
8. Click on cell H1, type: `layout`
9. Click on cell I1, type: `collection`
10. Click on cell J1, type: `thumbnail`
11. Click on cell K1, type: `full`
12. Click on cell L1, type: `manifest`
13. Click on cell M1, type: `video_url` (optional)
14. Click on cell N1, type: `audio_url` (optional)

---

## Example Rows (Fill In Row 2, 3, 4, etc.)

Here's how Row 2 should look (each value in its own column):

| pid | title | artist | date | description | medium | location | layout | collection | thumbnail | full | manifest | video_url | audio_url |
|-----|-------|--------|------|-------------|--------|----------|--------|------------|-----------|------|----------|-----------|-----------|
| artwork1 | Sunset Over Damascus | Ahmed Ali | 2020 | A beautiful painting showing the sunset | Oil Painting | Damascus | syrian_refugee_art_item | syrian_refugee_art | | | | | |

**Row 3:**
| pid | title | artist | date | description | medium | location | layout | collection | thumbnail | full | manifest |
|-----|-------|--------|------|-------------|--------|----------|--------|------------|-----------|------|----------|
| artwork2 | Refugee Camp Life | Samira Hassan | 2019 | Daily life in the refugee camp | Photography | Jordan | syrian_refugee_art_item | syrian_refugee_art | | | |

**Row 4:**
| pid | title | artist | date | description | medium | location | layout | collection | thumbnail | full | manifest |
|-----|-------|--------|------|-------------|--------|----------|--------|------------|-----------|------|----------|
| artwork3 | Hope | Mohammed | 2021 | A portrait expressing hope | Drawing | Lebanon | syrian_refugee_art_item | syrian_refugee_art | | | |

**In Google Sheets, it will look like this:**

```
     A          B                    C            D      E                              F              G          H                        I                      J    K    L
1   pid        title                 artist       date   description                     medium         location   layout                   collection            thumb full mani
2   artwork1   Sunset Over Damascus  Ahmed Ali    2020   A beautiful painting...       Oil Painting  Damascus   syrian_refugee_art_item  syrian_refugee_art
3   artwork2   Refugee Camp Life     Samira       2019   Daily life in the camp...      Photography   Jordan     syrian_refugee_art_item  syrian_refugee_art
4   artwork3   Hope                  Mohammed     2021   A portrait expressing...       Drawing       Lebanon    syrian_refugee_art_item  syrian_refugee_art
```

**Important:** Each piece of information goes in its own column. Don't combine multiple items in one cell!

**Notes:**
- Replace `artwork1`, `artwork2`, etc. with your own unique IDs
- Fill in your actual artwork information (title, artist, date, etc.)
- **Keep `layout` and `collection` the same for all rows** (copy exactly as shown)
- **Leave `thumbnail`, `full`, and `manifest` empty** (we'll fill these later)

---

## Quick Reference: What Goes Where

| Column | What to Put | Example |
|--------|-------------|---------|
| `pid` | Unique ID for each artwork | `artwork1`, `photo1`, `art001` |
| `title` | Artwork title | `Sunset Over Damascus` |
| `artist` | Artist name | `Ahmed Ali` |
| `date` | Year or date | `2020` or `2020-05-15` |
| `description` | Description of artwork | `A beautiful painting...` |
| `medium` | Type of art | `Photography`, `Oil Painting`, `Drawing` |
| `location` | Where it's from | `Damascus`, `Jordan`, `Lebanon` |
| `layout` | **Always:** `syrian_refugee_art_item` | `syrian_refugee_art_item` |
| `collection` | **Always:** `syrian_refugee_art` | `syrian_refugee_art` |
| `thumbnail` | **Leave empty** (or use for video poster) | (empty) |
| `full` | **Leave empty** | (empty) |
| `manifest` | **Leave empty** | (empty) |
| `video_url` | **For videos:** YouTube/Vimeo URL or file path | `https://youtube.com/...` or `/media/video1.mp4` |
| `audio_url` | **For audio:** File path to audio file | `/media/audio1.mp3` |

---

## Important Rules

✅ **DO:**
- Use the same `layout` value for all rows: `syrian_refugee_art_item`
- Use the same `collection` value for all rows: `syrian_refugee_art`
- Make each `pid` unique (no duplicates!)
- Use lowercase for `pid` (e.g., `artwork1` not `Artwork1`)

❌ **DON'T:**
- Don't change `layout` or `collection` values
- Don't use spaces in `pid` (use underscores: `artwork_1`)
- Don't fill in `thumbnail`, `full`, or `manifest` columns

---

## After You Fill In Your Sheet

1. **Export as CSV:**
   - File → Download → Comma-separated values (.csv)
   - Save as: `syrian_refugee_art.csv`

2. **Save it to:**
   - `syrian-refugee-art/_data/syrian_refugee_art.csv`

3. **Download your images:**
   - From Google Slides, download each image
   - Name each image to match the `pid` (e.g., `artwork1.jpg` for `pid: artwork1`)
   - Save all images in: `_data/raw_images/syrian_refugee_art/`

4. **Tell me when you're done!** I'll set up the rest for you.

