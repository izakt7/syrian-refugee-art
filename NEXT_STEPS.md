# Next Steps: Finishing Your Collection Setup

You're almost there! Here's exactly what to do next.

---

## ✅ What You've Already Done

- ✅ Created your Google Sheet with artwork information
- ✅ Uploaded 10 images to `_data/raw_images/syrian_refugee_art/`
  - artwork1.jpg through artwork10.jpg

---

## Step 1: Finish Your Google Sheet

Make sure your sheet has:

**Required columns:**
- `pid` - Must match your image filenames (artwork1, artwork2, etc.)
- `title` - Artwork title
- `layout` - Put `syrian_refugee_art_item` in every row
- `collection` - Put `syrian_refugee_art` in every row
- `thumbnail`, `full`, `manifest` - Leave these empty for now

**Optional columns:**
- `artist`, `date`, `description`, `medium`, `location`
- `video_url`, `audio_url` (if you have videos/audio)

**Important:** Make sure your `pid` values match your image filenames:
- If image is `artwork1.jpg` → CSV `pid` should be `artwork1`
- If image is `artwork2.jpg` → CSV `pid` should be `artwork2`
- And so on...

---

## Step 2: Export Your Google Sheet as CSV

1. In Google Sheets, go to **File** → **Download** → **Comma-separated values (.csv)**
2. Save the file as: `syrian_refugee_art.csv`
3. **Important:** Make sure the filename is exactly `syrian_refugee_art.csv` (lowercase, underscores)

---

## Step 3: Put the CSV File in the Right Place

**Move your CSV file here:**
```
syrian-refugee-art/
  _data/
    syrian_refugee_art.csv  ← Put it here!
```

**How to do it:**
1. Find your downloaded `syrian_refugee_art.csv` file
2. Copy or move it to: `syrian-refugee-art/_data/syrian_refugee_art.csv`
3. Make sure it's in the `_data` folder (same folder as `qatar.csv`)

---

## Step 4: Share Your CSV File With Me

Once your CSV file is in place, I can:
1. ✅ Update `_config.yml` to configure your collection
2. ✅ Generate all the collection pages
3. ✅ Process your images for web display
4. ✅ Set up the search index
5. ✅ Make sure everything works!

**Just let me know when your CSV file is ready!**

---

## What I'll Do For You

Once you have the CSV file in place, I'll run these commands:

1. **Update `_config.yml`** - Add your collection configuration
2. **Generate pages** - `bundle exec rake wax:pages syrian_refugee_art`
3. **Process images** - `bundle exec rake wax:derivatives:iiif syrian_refugee_art`
4. **Update CSV paths** - Fix the thumbnail/full/manifest paths
5. **Regenerate pages** - Update pages with correct image paths
6. **Create search index** - `bundle exec rake wax:search`

---

## Quick Checklist

Before you're ready:

- [ ] Google Sheet has all 10 artworks (rows)
- [ ] Every row has `layout: syrian_refugee_art_item`
- [ ] Every row has `collection: syrian_refugee_art`
- [ ] Every `pid` matches image filename (artwork1, artwork2, etc.)
- [ ] Images are named correctly (artwork1.jpg, artwork2.jpg, etc.)
- [ ] CSV file exported from Google Sheets
- [ ] CSV file saved as `syrian_refugee_art.csv`
- [ ] CSV file moved to `_data/` folder

---

## After I Set Everything Up

Once I'm done, you can:

1. **Preview your site:**
   ```bash
   bundle exec jekyll serve
   ```
   Then visit: `http://localhost:4000/syrian_refugee_art/artwork1/`

2. **Browse your collection:**
   - Visit: `http://localhost:4000/collection/`
   - See all 10 artworks

3. **Test search:**
   - Visit: `http://localhost:4000/search/`
   - Search for your artworks

---

## Need Help?

If you run into any issues:
- CSV not exporting correctly? Make sure you're using File → Download → CSV
- Images not matching? Check that `pid` values exactly match filenames
- File won't save? Make sure you have write permissions

**Just let me know when your CSV is ready and I'll take care of the rest!** 🎨

