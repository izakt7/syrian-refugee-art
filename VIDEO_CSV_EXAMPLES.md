# How to Fill Out Your CSV for Videos

## Quick Answer

**For videos, you still need:**
- ✅ `pid` - A unique ID (like `video1`, `video2`)
- ✅ `title`, `artist`, `date`, etc. - Your artwork information
- ✅ `layout` - `syrian_refugee_art_item`
- ✅ `collection` - `syrian_refugee_art`
- ✅ `video_url` - The YouTube/Vimeo URL or file path

**For videos, you can leave empty:**
- `thumbnail` - Leave empty (or use for poster image)
- `full` - Leave empty
- `manifest` - Leave empty

---

## Examples

### Example 1: YouTube Video

| pid | title | artist | date | video_url | layout | collection | thumbnail | full | manifest |
|-----|-------|--------|------|-----------|--------|------------|-----------|------|----------|
| video1 | Artist Interview | Ahmed Ali | 2020 | https://www.youtube.com/watch?v=ABC123 | syrian_refugee_art_item | syrian_refugee_art | | | |

**What to fill:**
- `pid`: `video1` (unique ID, doesn't need to match a filename)
- `title`: Your video title
- `artist`: Artist name
- `date`: Date/year
- `video_url`: YouTube URL
- `layout`: `syrian_refugee_art_item`
- `collection`: `syrian_refugee_art`
- `thumbnail`, `full`, `manifest`: Leave empty

---

### Example 2: Direct Video File

| pid | title | artist | date | video_url | thumbnail | layout | collection | full | manifest |
|-----|-------|--------|------|-----------|-----------|--------|------------|------|----------|
| video1 | My Video | Samira | 2021 | /assets/media/video1.mp4 | /assets/media/video1-poster.jpg | syrian_refugee_art_item | syrian_refugee_art | | |

**What to fill:**
- `pid`: `video1` (unique ID)
- `title`: Your video title
- `video_url`: `/assets/media/video1.mp4` (path to video file)
- `thumbnail`: Optional - poster image (like a thumbnail/preview image)
- `layout`: `syrian_refugee_art_item`
- `collection`: `syrian_refugee_art`
- `full`, `manifest`: Leave empty

---

### Example 3: Mixed Collection (Images + Videos)

| pid | title | artist | video_url | layout | collection | thumbnail | full | manifest |
|-----|-------|--------|-----------|--------|------------|-----------|------|----------|
| artwork1 | Sunset Painting | Ahmed | | syrian_refugee_art_item | syrian_refugee_art | | | |
| video1 | Artist Interview | Ahmed | https://youtube.com/watch?v=ABC123 | syrian_refugee_art_item | syrian_refugee_art | | | |
| artwork2 | Refugee Camp | Samira | | syrian_refugee_art_item | syrian_refugee_art | | | |

**Key points:**
- Images: Fill `thumbnail`, `full`, `manifest` (leave `video_url` empty)
- Videos: Fill `video_url` (leave `thumbnail`, `full`, `manifest` empty)
- Both: Use same `layout` and `collection`

---

## Complete CSV Column Guide for Videos

### Required Columns (Must Fill)

| Column | What to Put | Example |
|--------|-------------|---------|
| `pid` | Unique ID for the video | `video1`, `interview1`, `art_video1` |
| `title` | Video title | `Artist Interview` |
| `layout` | Always: `syrian_refugee_art_item` | `syrian_refugee_art_item` |
| `collection` | Always: `syrian_refugee_art` | `syrian_refugee_art` |
| `video_url` | YouTube/Vimeo URL or file path | `https://youtube.com/...` or `/assets/media/video1.mp4` |

### Optional Columns (Fill If You Have Info)

| Column | What to Put | Example |
|--------|-------------|---------|
| `artist` | Artist/creator name | `Ahmed Ali` |
| `date` | Date/year | `2020` |
| `description` | Description | `An interview with the artist...` |
| `medium` | Type | `Video`, `Documentary`, `Interview` |
| `location` | Location | `Damascus`, `Jordan` |
| `thumbnail` | Poster image (optional) | `/assets/media/video1-poster.jpg` |

### Leave Empty (For Videos)

| Column | What to Do |
|--------|-----------|
| `full` | Leave empty |
| `manifest` | Leave empty |

**Note:** `thumbnail` can be used for a poster/preview image for videos, but it's optional.

---

## Your Complete CSV Structure

Here's what your Google Sheet should look like with videos:

**Row 1 (Headers):**
```
pid,title,artist,date,description,medium,location,layout,collection,thumbnail,full,manifest,video_url,audio_url
```

**Row 2 (Image example):**
```
artwork1,Sunset Painting,Ahmed Ali,2020,A beautiful painting,Oil Painting,Damascus,syrian_refugee_art_item,syrian_refugee_art,,,,
```

**Row 3 (Video example):**
```
video1,Artist Interview,Ahmed Ali,2020,Interview with the artist,Video,Damascus,syrian_refugee_art_item,syrian_refugee_art,,,https://www.youtube.com/watch?v=ABC123,
```

**Row 4 (Another image):**
```
artwork2,Refugee Camp,Samira,2019,Daily life photo,Photography,Jordan,syrian_refugee_art_item,syrian_refugee_art,,,,
```

---

## Important Rules

✅ **DO:**
- Use unique `pid` values (video1, video2, etc.)
- Fill `video_url` for videos
- Use same `layout` and `collection` for all items
- Leave `full` and `manifest` empty for videos

❌ **DON'T:**
- Don't use the same `pid` twice
- Don't fill both `video_url` AND image columns for the same item (pick one)
- Don't worry about matching `pid` to a filename for videos (only images need that)

---

## Summary

**For videos:**
- `pid`: Any unique ID (like `video1`)
- `video_url`: YouTube/Vimeo URL or file path
- `thumbnail`, `full`, `manifest`: Leave empty (or use `thumbnail` for poster image)
- Everything else: Fill normally (title, artist, date, etc.)

**For images:**
- `pid`: Must match filename (artwork1 = artwork1.jpg)
- `thumbnail`, `full`, `manifest`: Will be filled automatically later
- `video_url`: Leave empty

The system automatically detects if it's a video (checks `video_url` first) or image!

