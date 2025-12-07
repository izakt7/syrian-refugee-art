# Simple Setup Guide: From Google Sheets to Your Collection

This guide walks you through setting up your collection when you have:
- ✅ An empty Google Sheet ready to fill
- ✅ Images in Google Slides that you can download

---

## Part 1: Understanding the Basics (Super Simple)

Think of it like organizing a photo album:

1. **Collection Name** = The name of your photo album (e.g., "Syrian Refugee Art")
2. **Layout** = The template/style for how each photo page looks
3. **CSV File** = Your Google Sheet exported as a CSV file

**The Simple Rule:** Everything with the same collection name goes together.

---

## Part 2: Setting Up Your Google Sheet

### Step 1: Name Your Collection

Choose a simple name. Let's use: **`syrian_refugee_art`**

**Rules:**
- All lowercase
- Use underscores instead of spaces
- No special characters
- Keep it short

**Examples:**
- ✅ `syrian_refugee_art`
- ✅ `refugee_art`
- ✅ `artworks`
- ❌ `Syrian Refugee Art` (has spaces and capitals)
- ❌ `syrian-refugee-art` (has dashes)

### Step 2: Set Up Your Google Sheet Columns

In your Google Sheet, create these columns in the first row:

| pid | title | artist | date | description | medium | location | layout | collection | thumbnail | full | manifest |
|-----|-------|--------|------|-------------|--------|----------|--------|------------|-----------|------|----------|

**What each column means:**

**Required Columns (you MUST fill these):**
- **`pid`** - A unique ID for each artwork (like "artwork1", "artwork2", "photo1")
- **`layout`** - Put `syrian_refugee_art_item` in every row (same for all)
- **`collection`** - Put `syrian_refugee_art` in every row (same for all)
- **`thumbnail`** - Leave empty for now (we'll fill this later)
- **`full`** - Leave empty for now (we'll fill this later)
- **`manifest`** - Leave empty for now (we'll fill this later)

**Your Content Columns (fill with your artwork info):**
- **`title`** - The artwork title
- **`artist`** - Artist name
- **`date`** - Year or date
- **`description`** - Description of the artwork
- **`medium`** - Type (Photography, Painting, etc.)
- **`location`** - Where it was created or where it's from

### Step 3: Fill In Your Data

Here's an example of how to fill it out:

| pid | title | artist | date | description | medium | location | layout | collection | thumbnail | full | manifest |
|-----|-------|--------|------|-------------|--------|----------|--------|------------|-----------|------|----------|
| artwork1 | Sunset Over Damascus | Ahmed Ali | 2020 | A beautiful painting showing the sunset | Oil Painting | Damascus | syrian_refugee_art_item | syrian_refugee_art | | | |
| artwork2 | Refugee Camp Life | Samira Hassan | 2019 | Daily life in the camp | Photography | Jordan | syrian_refugee_art_item | syrian_refugee_art | | | |
| artwork3 | Hope | Mohammed | 2021 | A portrait expressing hope | Drawing | Lebanon | syrian_refugee_art_item | syrian_refugee_art | | | |

**Important Notes:**
- Every row must have the same `layout` value: `syrian_refugee_art_item`
- Every row must have the same `collection` value: `syrian_refugee_art`
- The `pid` must be unique for each artwork (no duplicates!)
- Leave `thumbnail`, `full`, and `manifest` empty for now

---

## Part 3: Downloading and Organizing Your Images

### Step 1: Download Images from Google Slides

1. Open your Google Slides with the images
2. For each image:
   - Right-click on the image
   - Select "Save image as..." or "Download image"
   - Save it with a name that matches the `pid` from your sheet

**Example:**
- If your sheet has `pid: artwork1`, save the image as `artwork1.jpg`
- If your sheet has `pid: artwork2`, save the image as `artwork2.jpg`
- If your sheet has `pid: photo1`, save the image as `photo1.jpg`

**File naming rules:**
- Use the EXACT same name as the `pid` column
- Use lowercase (match your `pid` exactly)
- Supported formats: `.jpg`, `.jpeg`, `.png`, `.tif`

### Step 2: Create the Images Folder

On your computer, create this folder structure:

```
syrian-refugee-art/
  _data/
    raw_images/
      syrian_refugee_art/    ← Create this folder
        artwork1.jpg          ← Put your images here
        artwork2.jpg
        artwork3.jpg
        ...
```

**Steps:**
1. Navigate to: `syrian-refugee-art/_data/raw_images/`
2. Create a new folder called: `syrian_refugee_art` (must match your collection name!)
3. Put all your downloaded images in this folder
4. Make sure image filenames match the `pid` values from your sheet

**Example:**
- Sheet says `pid: artwork1` → Image file should be `artwork1.jpg`
- Sheet says `pid: photo2` → Image file should be `photo2.jpg`

---

## Part 4: Export Your Google Sheet as CSV

1. In Google Sheets, go to **File** → **Download** → **Comma-separated values (.csv)**
2. Save it as: `syrian_refugee_art.csv`
3. Move this file to: `syrian-refugee-art/_data/`

**Final file structure should look like:**
```
syrian-refugee-art/
  _data/
    syrian_refugee_art.csv          ← Your exported Google Sheet
    raw_images/
      syrian_refugee_art/            ← Your images folder
        artwork1.jpg
        artwork2.jpg
        artwork3.jpg
        ...
```

---

## Part 5: Update the Configuration File

I'll help you update `_config.yml` to connect everything together. Here's what needs to match:

**In your CSV file:**
- `collection` column = `syrian_refugee_art`
- `layout` column = `syrian_refugee_art_item`

**In `_config.yml` (I'll set this up for you):**
```yaml
collections:
  syrian_refugee_art:  # ← Must match your CSV collection column
    output: true
    layout: 'syrian_refugee_art_item'  # ← Must match your CSV layout column
    metadata:
      source: 'syrian_refugee_art.csv'  # ← Your CSV filename
    images:
      source: 'raw_images/syrian_refugee_art'  # ← Your images folder name
```

**The Magic Connection:**
- Collection name in CSV = Collection name in `_config.yml` ✅
- Layout name in CSV = Layout file exists ✅
- Image filenames = `pid` values in CSV ✅

---

## Quick Checklist

Before you're ready, make sure:

- [ ] Google Sheet has all required columns
- [ ] Every row has `layout: syrian_refugee_art_item`
- [ ] Every row has `collection: syrian_refugee_art`
- [ ] Every `pid` is unique
- [ ] Images downloaded and named to match `pid` values
- [ ] Images saved in `_data/raw_images/syrian_refugee_art/` folder
- [ ] Google Sheet exported as `syrian_refugee_art.csv`
- [ ] CSV file saved in `_data/` folder

---

## What Happens Next

Once you have:
1. ✅ Your CSV file in `_data/`
2. ✅ Your images in `_data/raw_images/syrian_refugee_art/`

I can:
1. Update `_config.yml` for you
2. Generate all the pages
3. Process your images
4. Set everything up!

Just share your CSV file and let me know when your images are ready!

---

## Common Questions

**Q: What if I have 50 artworks?**
A: Fill out 50 rows in your Google Sheet, one per artwork. Download 50 images, name them to match the `pid` values.

**Q: Can I use different image formats?**
A: Yes! `.jpg`, `.jpeg`, `.png`, `.tif` all work. Just make sure the filename matches the `pid`.

**Q: What if I make a mistake in the sheet?**
A: No problem! Just fix it in Google Sheets, re-export the CSV, and replace the old one.

**Q: Do I need to fill thumbnail, full, and manifest columns?**
A: No! Leave them empty. These get filled automatically when we process the images.

**Q: Can I add more columns?**
A: Yes! Add any columns you want (like `year`, `category`, `tags`). Just make sure to include the required ones.

---

## Example: Complete Workflow

**Step 1:** Open Google Sheet, create columns, fill in 3 artworks:
```
pid: artwork1, artwork2, artwork3
title: "Sunset", "Camp Life", "Hope"
artist: "Ahmed", "Samira", "Mohammed"
layout: syrian_refugee_art_item (all rows)
collection: syrian_refugee_art (all rows)
```

**Step 2:** Download 3 images from Google Slides:
- Save as: `artwork1.jpg`, `artwork2.jpg`, `artwork3.jpg`

**Step 3:** Create folder and move images:
- Create: `_data/raw_images/syrian_refugee_art/`
- Move images there

**Step 4:** Export sheet as CSV:
- File → Download → CSV
- Save as: `syrian_refugee_art.csv`
- Move to: `_data/`

**Step 5:** Tell me you're ready, and I'll do the rest! 🎉

