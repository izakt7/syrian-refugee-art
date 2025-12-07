# How to Replace Template Content with Your Own Collection

This guide will teach you how to customize your Wax exhibition site by replacing the template's demo content (the "qatar" collection) with your own images and metadata.

## Understanding the Wax Structure

A Wax site has two main components:
1. **Collection Items** - Individual artworks/objects with metadata (like the `qatar` collection)
2. **Exhibits** - Curated pages that tell stories using collection items (like `_exhibits/a.md` and `_exhibits/b.md`)

---

## Part 1: Replacing the Collection

### Step 1: Prepare Your Metadata File

Your metadata file is a CSV file located in `_data/`. Currently, you have `qatar.csv`. 

**What you need to do:**
1. Create a new CSV file in `_data/` (e.g., `my_collection.csv`)
2. The first row must be column headers
3. Each subsequent row represents one item in your collection

**Required columns:**
- `pid` - A unique identifier for each item (e.g., "artwork1", "photo001")
- `thumbnail` - Path to thumbnail image (will be auto-generated, but you can set a placeholder)
- `full` - Path to full-size image (will be auto-generated)
- `manifest` - Path to IIIF manifest (will be auto-generated)
- `layout` - The layout template to use (e.g., "qatar_item" or create your own)
- `collection` - The collection name (must match what you configure in `_config.yml`)

**Optional columns** (customize based on your needs):
- `artist`, `title`, `label`, `description`, `date`, `location`, `medium`, etc.
- Any metadata fields relevant to your collection

**Example CSV structure:**
```csv
pid,title,artist,date,description,layout,collection,thumbnail,full,manifest
artwork1,Sunset Over Damascus,Ahmed Ali,2020,"A beautiful painting...",my_item,my_collection,/img/derivatives/iiif/images/artwork1/full/250,/0/default.jpg,/img/derivatives/iiif/images/artwork1/full/1140,/0/default.jpg,/img/derivatives/iiif/artwork1/manifest.json
artwork2,Refugee Camp,Samira Hassan,2019,"Photograph showing...",my_item,my_collection,/img/derivatives/iiif/images/artwork2/full/250,/0/default.jpg,/img/derivatives/iiif/images/artwork2/full/1140,/0/default.jpg,/img/derivatives/iiif/artwork2/manifest.json
```

**Important:** The `thumbnail`, `full`, and `manifest` paths will be automatically generated when you run the image processing tasks, so you can use placeholders initially.

### Step 2: Organize Your Image Files

**Current structure:**
```
_data/
  raw_images/
    qatar/
      obj1.jpg
      obj2.jpg
      ...
```

**What you need to do:**
1. Create a new folder in `_data/raw_images/` (e.g., `my_collection/`)
2. Place all your image files in this folder
3. **Critical:** Name your image files to match the `pid` values in your CSV
   - If your CSV has `pid: artwork1`, name the file `artwork1.jpg` (or `.png`, `.tif`, etc.)
   - If your CSV has `pid: photo001`, name the file `photo001.jpg`

**Example:**
```
_data/
  raw_images/
    my_collection/
      artwork1.jpg
      artwork2.jpg
      artwork3.png
      ...
```

**Supported formats:** JPG, PNG, TIFF, PDF (for multi-page documents)

**For multi-page documents** (like PDFs):
- If you have `obj12.pdf` with multiple pages, create a folder `obj12/` and place numbered images inside:
  ```
  obj12/
    00.jpg
    01.jpg
    02.jpg
    ...
  ```

### Step 3: Update `_config.yml`

Open `_config.yml` and find the `collections:` section (around line 59).

**Current configuration:**
```yaml
collections:
  exhibits:
    output: true
  qatar: # name of collection
    output: true
    layout: 'qatar_item'
    metadata:
      source: 'qatar.csv'
    images:
      source: 'raw_images/qatar'
```

**What to change:**
1. Replace `qatar` with your collection name (e.g., `my_collection`)
2. Update `layout` to match your layout file (or keep `qatar_item` if you're using that)
3. Update `metadata.source` to your CSV filename
4. Update `images.source` to your images folder path

**Example:**
```yaml
collections:
  exhibits:
    output: true
  my_collection: # your collection name
    output: true
    layout: 'qatar_item' # or create 'my_collection_item'
    metadata:
      source: 'my_collection.csv' # your CSV file
    images:
      source: 'raw_images/my_collection' # your images folder
```

**Also update the search configuration** (around line 78):
```yaml
search:
  main:
    index: '/search/index.json'
    collections:
      my_collection: # change from 'qatar' to your collection name
        content: false
        fields: # update these to match your CSV columns
          - artist
          - title
          - date
          - description
```

**Update the menu** (around line 99) to point to your collection:
```yaml
menu:
  - label: 'Browse'
    link: '/collection/' # This will show all items in your collection
```

### Step 4: Generate Collection Pages

After setting up your metadata and images, you need to generate the individual item pages.

**Run this command:**
```bash
bundle exec rake wax:pages my_collection
```

Replace `my_collection` with whatever you named your collection in `_config.yml`.

**What this does:**
- Reads your CSV file
- Creates individual markdown files in `_my_collection/` folder (or `_qatar/` if you kept that name)
- Each file corresponds to one row in your CSV

**Example output:**
```
_my_collection/
  artwork1.md
  artwork2.md
  artwork3.md
  ...
```

### Step 5: Generate Image Derivatives

Wax needs to process your images into web-friendly formats with zoom capabilities.

**Run this command:**
```bash
bundle exec rake wax:derivatives:iiif my_collection
```

Replace `my_collection` with your collection name.

**What this does:**
- Processes all images in `_data/raw_images/my_collection/`
- Creates optimized versions in `img/derivatives/iiif/`
- Generates IIIF manifests for zoom/pan functionality
- Takes time depending on number and size of images

**Important:** After running this, update your CSV file with the correct paths. The paths should follow this pattern:
- `thumbnail`: `/img/derivatives/iiif/images/{pid}/full/250,/0/default.jpg`
- `full`: `/img/derivatives/iiif/images/{pid}/full/1140,/0/default.jpg`
- `manifest`: `/img/derivatives/iiif/{pid}/manifest.json`

### Step 6: Update Collection Item Layout (Optional)

If you want a custom layout for your collection items, you can:

1. Copy `_layouts/qatar_item.html` to `_layouts/my_collection_item.html`
2. Customize the HTML/Liquid template as needed
3. Update `_config.yml` to use `layout: 'my_collection_item'`

---

## Part 2: Replacing Exhibits

Exhibits are curated pages that tell stories using your collection items.

### Step 1: Edit Existing Exhibits

**Current exhibits:**
- `_exhibits/a.md` - Example exhibit with parallax image
- `_exhibits/b.md` - Example exhibit with inline images

**What to change:**

1. **Update the front matter** (YAML at the top):
```yaml
---
layout: exhibit
title: 'My Exhibit: Syrian Refugee Art'
author: Your Name
publish_date: 2024-01-15
permalink: /exhibits/my-exhibit/
---
```

2. **Replace the content** with your own text

3. **Update image references** to use your collection:
   - Change `collection='qatar'` to `collection='my_collection'`
   - Change `pid='obj1'` to `pid='artwork1'` (use your actual pids)

**Example:**
```markdown
{% include parallax_image.html collection='my_collection' pid='artwork1' y='50%' clickable='true' %}
```

or

```markdown
{% include inline_image.html collection='my_collection' pid='artwork2' clickable='true' %}
```

### Step 2: Create New Exhibits

1. Create a new `.md` file in `_exhibits/` folder
2. Use the same structure as existing exhibits
3. Reference your collection items using the include tags

**Available include tags:**
- `{% include parallax_image.html collection='my_collection' pid='artwork1' y='50%' clickable='true' %}` - Parallax scrolling image
- `{% include inline_image.html collection='my_collection' pid='artwork1' clickable='true' %}` - Regular inline image
- `{% include osd_iiif_image_viewer.html collection='my_collection' pid='artwork1' %}` - Zoomable IIIF viewer

### Step 3: Update Menu

In `_config.yml`, update the menu to link to your exhibits:

```yaml
menu:
  - label: 'Exhibits'
    sub:
      - label: 'My First Exhibit'
        link: '/exhibits/my-exhibit/'
      - label: 'My Second Exhibit'
        link: '/exhibits/my-second-exhibit/'
```

---

## Part 3: Updating Other Content

### Update Site Information

In `_config.yml`, update:
- `title` - Your site title
- `description` - Site description
- `url` - Your site URL
- `baseurl` - Base URL path (if deploying to GitHub Pages)
- `copyright` - Copyright information
- `logo` - Path to your logo image

### Update Pages

Edit files in `pages/`:
- `about.md` - About page
- `collection.md` - Collection browse page (usually auto-generated)
- `credits.md` - Credits page
- `reuse.md` - Reuse/licensing information

### Update Search Index

After making changes, regenerate the search index:

```bash
bundle exec rake wax:search
```

This creates/updates `search/index.json` with searchable content from your collections.

---

## Part 4: Complete Workflow Summary

Here's the complete process in order:

1. **Prepare metadata CSV** → Create `_data/my_collection.csv`
2. **Organize images** → Place images in `_data/raw_images/my_collection/`
3. **Update `_config.yml`** → Configure collection settings
4. **Generate pages** → `bundle exec rake wax:pages my_collection`
5. **Generate image derivatives** → `bundle exec rake wax:derivatives:iiif my_collection`
6. **Update CSV with correct paths** → Fix thumbnail/full/manifest paths
7. **Regenerate pages** → `bundle exec rake wax:pages my_collection` (again, to pick up path changes)
8. **Update exhibits** → Edit `_exhibits/*.md` files
9. **Regenerate search** → `bundle exec rake wax:search`
10. **Preview site** → `bundle exec jekyll serve`

---

## Troubleshooting

**Images not showing?**
- Check that image filenames match `pid` values in CSV
- Verify image derivatives were generated: check `img/derivatives/iiif/` folder
- Ensure paths in CSV match the generated structure

**Pages not generating?**
- Check CSV syntax (no extra commas, proper quotes)
- Verify collection name in `_config.yml` matches what you're using in rake commands
- Check that `pid` column exists and has unique values

**Search not working?**
- Run `bundle exec rake wax:search` after making changes
- Verify search fields in `_config.yml` match your CSV column names

**Layout issues?**
- Check that `layout` value in CSV matches a file in `_layouts/`
- Verify collection name in include tags matches your collection name

---

## Next Steps

- Read the [Wax documentation](https://minicomp.github.io/wiki/wax/) for advanced customization
- Customize layouts in `_layouts/`
- Customize styling in `_sass/` and `assets/styles.scss`
- Add custom includes in `_includes/`

Good luck with your exhibition!

