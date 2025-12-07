# Understanding Layout and Collection Columns

This guide explains how to use the `layout` and `collection` columns in your CSV metadata file.

---

## The `collection` Column

### What It Is
The `collection` column identifies which collection an item belongs to. This must match the collection name defined in `_config.yml`.

### How to Use It

### Step-by-Step: Setting Up Your Collection Name

**Think of it like naming a photo album - you need one name that you'll use everywhere.**

#### Step 1: Choose Your Collection Name

Pick a simple name. For example: **`syrian_refugee_art`**

**Rules:**
- ✅ All lowercase letters
- ✅ Use underscores `_` instead of spaces
- ✅ No special characters (no dashes, dots, etc.)
- ✅ Keep it short (like a folder name)

**Good examples:**
- `syrian_refugee_art`
- `refugee_art`
- `artworks`

**Bad examples:**
- `Syrian Refugee Art` (has capitals and spaces)
- `syrian-refugee-art` (has dashes)
- `syrian.refugee.art` (has dots)

#### Step 2: Put It in Your Google Sheet (CSV)

In your Google Sheet, create a column called `collection` and fill every row with the same name:

| pid | title | artist | collection |
|-----|-------|--------|------------|
| artwork1 | Sunset | Ahmed Ali | syrian_refugee_art |
| artwork2 | Camp Life | Samira | syrian_refugee_art |
| artwork3 | Hope | Mohammed | syrian_refugee_art |

**Important:** Every single row must have the exact same collection name!

#### Step 3: Create Your Images Folder

Create a folder with the same name as your collection:

**Folder path:** `_data/raw_images/syrian_refugee_art/`

**Steps:**
1. Go to: `syrian-refugee-art/_data/raw_images/`
2. Create a new folder
3. Name it exactly: `syrian_refugee_art` (must match your collection name!)
4. Put all your images in this folder

#### Step 4: Match It in `_config.yml`

The collection name must appear in `_config.yml` too. Here's what it looks like:

```yaml
collections:
  syrian_refugee_art:  # ← This must match your CSV collection column
    output: true
    layout: 'syrian_refugee_art_item'
    metadata:
      source: 'syrian_refugee_art.csv'  # ← Your CSV filename
    images:
      source: 'raw_images/syrian_refugee_art'  # ← Your images folder name
```

**The Connection:**
- Collection name in Google Sheet = Collection name in `_config.yml` ✅
- Collection name in Google Sheet = Images folder name ✅

**Example:**
- Google Sheet has: `collection: syrian_refugee_art`
- `_config.yml` has: `syrian_refugee_art:`
- Images folder is: `raw_images/syrian_refugee_art/`
- ✅ All match = Everything works!

**Important:** All items in the same CSV file should have the same `collection` value.

---

## The `layout` Column

### What It Is
The `layout` column tells Jekyll which layout template file to use when displaying each item's page. The layout controls how the page looks and what metadata fields are displayed.

### How to Use It

#### Option 1: Use an Existing Layout (Easiest)

You can use one of these existing layouts:

1. **`generic_collection_item`** - A flexible layout that works with any metadata
2. **`qatar_item`** - The template's existing layout (you can reuse it)

**In your CSV:**
```csv
pid,title,artist,layout,collection,...
artwork1,Sunset,Ahmed Ali,generic_collection_item,syrian_refugee_art,...
artwork2,Refugee Camp,Samira,generic_collection_item,syrian_refugee_art,...
```

#### Option 2: Create Your Own Custom Layout (More Control)

**Step 1:** Copy an existing layout as a starting point:
```bash
cp _layouts/qatar_item.html _layouts/syrian_refugee_art_item.html
```

**Step 2:** Edit `_layouts/syrian_refugee_art_item.html` to customize:

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

**What this does:**
- `layout: generic_collection_item` - Uses the base layout template
- `pagination: true` - Shows prev/next navigation between items
- `meta:` - Defines which metadata fields to display and their labels

**Step 3:** Use your custom layout in the CSV:
```csv
pid,title,artist,layout,collection,...
artwork1,Sunset,Ahmed Ali,syrian_refugee_art_item,syrian_refugee_art,...
artwork2,Refugee Camp,Samira,syrian_refugee_art_item,syrian_refugee_art,...
```

**Step 4:** Update `_config.yml` to use this layout as default:
```yaml
collections:
  syrian_refugee_art:
    output: true
    layout: 'syrian_refugee_art_item'  # ← Your custom layout
    metadata:
      source: 'syrian_refugee_art.csv'
    images:
      source: 'raw_images/syrian_refugee_art'
```

---

## Complete Example

Let's say you want to create a collection called `syrian_refugee_art`:

### 1. Create Your CSV File (`_data/syrian_refugee_art.csv`)

```csv
pid,title,artist,date,description,medium,location,layout,collection,thumbnail,full,manifest
artwork1,Sunset Over Damascus,Ahmed Ali,2020,"A beautiful painting depicting...",Oil Painting,Damascus,syrian_refugee_art_item,syrian_refugee_art,/img/derivatives/iiif/images/artwork1/full/250,/0/default.jpg,/img/derivatives/iiif/images/artwork1/full/1140,/0/default.jpg,/img/derivatives/iiif/artwork1/manifest.json
artwork2,Refugee Camp,Samira Hassan,2019,"Photograph showing daily life...",Photography,Jordan,syrian_refugee_art_item,syrian_refugee_art,/img/derivatives/iiif/images/artwork2/full/250,/0/default.jpg,/img/derivatives/iiif/images/artwork2/full/1140,/0/default.jpg,/img/derivatives/iiif/artwork2/manifest.json
```

**Key points:**
- `layout: syrian_refugee_art_item` - Uses your custom layout
- `collection: syrian_refugee_art` - All items have the same collection name
- `thumbnail`, `full`, `manifest` - Paths will be auto-generated (use these placeholders initially)

### 2. Create Your Custom Layout (`_layouts/syrian_refugee_art_item.html`)

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

### 3. Update `_config.yml`

```yaml
collections:
  exhibits:
    output: true
  syrian_refugee_art:  # ← Collection name (matches CSV)
    output: true
    layout: 'syrian_refugee_art_item'  # ← Your layout file name (without .html)
    metadata:
      source: 'syrian_refugee_art.csv'  # ← Your CSV file
    images:
      source: 'raw_images/syrian_refugee_art'  # ← Your images folder

search:
  main:
    index: '/search/index.json'
    collections:
      syrian_refugee_art:  # ← Collection name again
        content: false
        fields:  # ← Fields from your CSV to make searchable
          - title
          - artist
          - date
          - description
          - medium
```

### 4. Organize Your Images

Place images in: `_data/raw_images/syrian_refugee_art/`
- Name files to match `pid` values: `artwork1.jpg`, `artwork2.jpg`, etc.

---

## Quick Reference

### Collection Column
- **Purpose:** Groups items together
- **Format:** lowercase_with_underscores (e.g., `syrian_refugee_art`)
- **Must match:** Collection name in `_config.yml`
- **Same for all:** All items in one CSV should have the same collection name

### Layout Column
- **Purpose:** Controls how each item page looks
- **Format:** Layout filename without `.html` (e.g., `syrian_refugee_art_item`)
- **Options:** 
  - Use existing: `generic_collection_item` or `qatar_item`
  - Create custom: Make a file in `_layouts/` and reference it here
- **Can vary:** Different items can use different layouts (though usually all use the same)

---

## Common Questions

**Q: Can I use different layouts for different items?**
A: Yes! You can have `artwork1` use `layout1` and `artwork2` use `layout2`, but typically all items in a collection use the same layout.

**Q: Do I need to create a custom layout?**
A: No! You can use `generic_collection_item` which works with any metadata fields. Custom layouts give you more control over what's displayed.

**Q: What if I change the layout later?**
A: Just update the `layout` column in your CSV and regenerate pages with `bundle exec rake wax:pages syrian_refugee_art`

**Q: Can I have multiple collections?**
A: Yes! You can have multiple collections (e.g., `syrian_refugee_art` and `photography`). Each needs its own entry in `_config.yml` and its own CSV file.

---

## Next Steps

1. Decide on your collection name
2. Choose or create a layout
3. Set both values in your CSV
4. Update `_config.yml` to match
5. Run `bundle exec rake wax:pages your_collection_name` to generate pages

