# Quick Customization Checklist

Use this checklist as you replace the template content with your own collection.

## ✅ Collection Setup

- [ ] Created metadata CSV file in `_data/` (e.g., `my_collection.csv`)
- [ ] CSV has required columns: `pid`, `thumbnail`, `full`, `manifest`, `layout`, `collection`
- [ ] Added all metadata rows to CSV (one per item)
- [ ] Created images folder: `_data/raw_images/my_collection/`
- [ ] Named image files to match `pid` values (e.g., `artwork1.jpg` for `pid: artwork1`)
- [ ] Updated `_config.yml` collections section with new collection name
- [ ] Updated `_config.yml` search section with new collection name and fields
- [ ] Ran `bundle exec rake wax:pages my_collection` to generate pages
- [ ] Ran `bundle exec rake wax:derivatives:iiif my_collection` to process images
- [ ] Updated CSV with correct thumbnail/full/manifest paths
- [ ] Regenerated pages: `bundle exec rake wax:pages my_collection`
- [ ] Regenerated search: `bundle exec rake wax:search`

## ✅ Exhibits

- [ ] Updated `_exhibits/a.md` with your content
- [ ] Updated `_exhibits/b.md` with your content
- [ ] Changed `collection='qatar'` to `collection='my_collection'` in exhibits
- [ ] Changed `pid` values to match your collection items
- [ ] Created new exhibit files if needed
- [ ] Updated menu in `_config.yml` to link to your exhibits

## ✅ Site Information

- [ ] Updated `title` in `_config.yml`
- [ ] Updated `description` in `_config.yml`
- [ ] Updated `url` and `baseurl` in `_config.yml`
- [ ] Updated `copyright` in `_config.yml`
- [ ] Updated `logo` path in `_config.yml` (if you have a logo)
- [ ] Updated `pages/about.md`
- [ ] Updated `pages/credits.md`
- [ ] Updated `pages/reuse.md`
- [ ] Updated footer links in `_config.yml`

## ✅ Testing

- [ ] Ran `bundle exec jekyll serve` to preview site
- [ ] Checked that collection items display correctly
- [ ] Checked that images load and zoom works
- [ ] Tested search functionality
- [ ] Tested exhibit pages
- [ ] Checked navigation menu links
- [ ] Verified all images have correct paths

## 🎉 Final Steps

- [ ] Removed or archived old template files (optional)
- [ ] Committed changes to git
- [ ] Deployed to GitHub Pages or your hosting platform

---

**Quick Command Reference:**

```bash
# Generate collection pages
bundle exec rake wax:pages COLLECTION_NAME

# Generate image derivatives
bundle exec rake wax:derivatives:iiif COLLECTION_NAME

# Regenerate search index
bundle exec rake wax:search

# Preview site locally
bundle exec jekyll serve
```

Replace `COLLECTION_NAME` with your actual collection name (e.g., `my_collection`).

