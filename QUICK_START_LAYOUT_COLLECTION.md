# Quick Start: Layout & Collection Setup

## Visual Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    YOUR CSV FILE                            │
│  _data/syrian_refugee_art.csv                              │
│                                                             │
│  pid      │ layout              │ collection              │
│  ─────────┼─────────────────────┼─────────────────────────│
│  artwork1 │ syrian_refugee_art  │ syrian_refugee_art      │
│           │ _item               │                         │
│  artwork2 │ syrian_refugee_art  │ syrian_refugee_art      │
│           │ _item               │                         │
└───────────┴─────────────────────┴─────────────────────────┘
            │                      │
            │                      │
            ▼                      ▼
┌──────────────────────┐  ┌──────────────────────────────┐
│   LAYOUT FILE        │  │   _config.yml                 │
│   _layouts/          │  │                               │
│   syrian_refugee_    │  │   collections:                │
│   art_item.html      │  │     syrian_refugee_art:  ←───┐│
│                      │  │       layout: 'syrian_      ││
│   (Controls how      │  │         refugee_art_item'   ││
│    each item page    │  │       metadata:              ││
│    looks)            │  │         source: 'syrian_     ││
│                      │  │           refugee_art.csv'  ││
└──────────────────────┘  └──────────────────────────────┘
```

---

## Step-by-Step Setup

### Step 1: Choose Your Collection Name
**Example:** `syrian_refugee_art`

**Rules:**
- Use lowercase letters
- Use underscores instead of spaces
- Keep it short and descriptive
- This name will be used in multiple places

---

### Step 2: Create Your Layout File

**File location:** `_layouts/syrian_refugee_art_item.html`

**Content:**
```yaml
---
layout: generic_collection_item
pagination: true
meta:
  - label: 'Title'
    value: page.title
  - label: 'Artist'
    value: page.artist
  - label: 'Date'
    value: page.date
  - label: 'Description'
    value: page.description
  - label: 'Medium'
    value: page.medium
  - label: 'Location'
    value: page.location
---
```

**What to customize:**
- Change the `meta:` section to match your CSV columns
- Each `- label:` becomes a label in the metadata table
- Each `value: page.column_name` pulls data from your CSV

**Example:** If your CSV has a column called `year`, add:
```yaml
  - label: 'Year'
    value: page.year
```

---

### Step 3: Set Up Your CSV File

**File location:** `_data/syrian_refugee_art.csv`

**Required columns:**
- `pid` - Unique identifier (must match image filename)
- `layout` - Layout file name (without `.html`)
- `collection` - Collection name (must match `_config.yml`)
- `thumbnail`, `full`, `manifest` - Image paths (auto-generated later)

**Example row:**
```csv
pid,title,artist,date,description,medium,location,layout,collection,thumbnail,full,manifest
artwork1,Sunset Over Damascus,Ahmed Ali,2020,"Beautiful painting",Oil Painting,Damascus,syrian_refugee_art_item,syrian_refugee_art,/img/derivatives/iiif/images/artwork1/full/250,/0/default.jpg,/img/derivatives/iiif/images/artwork1/full/1140,/0/default.jpg,/img/derivatives/iiif/artwork1/manifest.json
```

**Key points:**
- `layout: syrian_refugee_art_item` ← Matches your layout file name (no `.html`)
- `collection: syrian_refugee_art` ← Matches collection name in `_config.yml`
- All rows should have the same `layout` and `collection` values

---

### Step 4: Update `_config.yml`

**Find the `collections:` section and add/update:**

```yaml
collections:
  exhibits:
    output: true
  syrian_refugee_art:  # ← Collection name (matches CSV)
    output: true
    layout: 'syrian_refugee_art_item'  # ← Layout name (matches CSV, no .html)
    metadata:
      source: 'syrian_refugee_art.csv'  # ← Your CSV filename
    images:
      source: 'raw_images/syrian_refugee_art'  # ← Your images folder
```

**Also update the search section:**

```yaml
search:
  main:
    index: '/search/index.json'
    collections:
      syrian_refugee_art:  # ← Collection name again
        content: false
        fields:  # ← List your CSV column names here
          - title
          - artist
          - date
          - description
          - medium
```

---

## The Connection Chain

1. **CSV `collection` column** → Must match → **`_config.yml` collection name**
2. **CSV `layout` column** → Must match → **Layout filename** (without `.html`)
3. **Layout `meta` fields** → Must match → **CSV column names**

**Example:**
- CSV has: `collection: syrian_refugee_art`
- `_config.yml` has: `syrian_refugee_art:`
- ✅ They match!

- CSV has: `layout: syrian_refugee_art_item`
- Layout file is: `_layouts/syrian_refugee_art_item.html`
- ✅ They match!

- Layout has: `value: page.title`
- CSV has column: `title`
- ✅ They match!

---

## Common Mistakes to Avoid

❌ **Wrong:** Collection name mismatch
```csv
collection: syrian_refugee_art  # In CSV
```
```yaml
collections:
  refugee_art:  # Different name in _config.yml
```
✅ **Right:** Same name everywhere

❌ **Wrong:** Layout name includes `.html`
```csv
layout: syrian_refugee_art_item.html  # Don't include .html
```
✅ **Right:** 
```csv
layout: syrian_refugee_art_item  # No .html extension
```

❌ **Wrong:** Layout references non-existent CSV column
```yaml
meta:
  - label: 'Year'
    value: page.year  # But CSV has 'date' not 'year'
```
✅ **Right:** Match CSV column names exactly

---

## Testing Your Setup

After setting everything up:

1. **Generate pages:**
   ```bash
   bundle exec rake wax:pages syrian_refugee_art
   ```

2. **Check generated files:**
   Look in `_syrian_refugee_art/` folder - you should see `.md` files for each item

3. **Preview site:**
   ```bash
   bundle exec jekyll serve
   ```

4. **Visit:** `http://localhost:4000/syrian_refugee_art/artwork1/` (or your baseurl)

If pages don't generate or look wrong, check:
- Collection name matches everywhere
- Layout file exists and is named correctly
- CSV column names match layout `meta` fields

---

## Summary

**Collection Column:**
- Groups items together
- Must match `_config.yml` collection name
- Same for all items in one CSV

**Layout Column:**
- Controls page appearance
- Must match layout filename (without `.html`)
- Usually same for all items in one collection

**The Flow:**
```
CSV → _config.yml → Layout File → Generated Pages
```

All three must be connected correctly!

