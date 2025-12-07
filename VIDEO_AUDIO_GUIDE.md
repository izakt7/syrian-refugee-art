# Adding Video and Audio to Your Collection

This guide explains how to add video and audio files as artworks in your collection.

---

## Overview

Your collection can include:
- ✅ **Images** (photos, paintings, drawings)
- ✅ **Videos** (YouTube, Vimeo, or direct video files)
- ✅ **Audio** (music, interviews, sound recordings)

All three types use the same CSV structure - you just fill in different columns!

---

## Part 1: Adding Videos

### Option 1: YouTube or Vimeo Videos (Easiest)

**In your Google Sheet, add a `video_url` column:**

| pid | title | artist | video_url | layout | collection |
|-----|-------|--------|-----------|--------|------------|
| video1 | Interview with Artist | Ahmed Ali | https://www.youtube.com/watch?v=ABC123 | syrian_refugee_art_item | syrian_refugee_art |
| video2 | Art Process | Samira | https://vimeo.com/123456789 | syrian_refugee_art_item | syrian_refugee_art |

**Supported formats:**
- YouTube: `https://www.youtube.com/watch?v=VIDEO_ID` or `https://youtu.be/VIDEO_ID`
- Vimeo: `https://vimeo.com/VIDEO_ID`

**What happens:**
- The video will be embedded and play directly on your site
- No need to download or host the video yourself!

### Option 2: Direct Video Files

**If you have video files (MP4, WebM, OGG):**

1. **Create a media folder:**
   ```
   syrian-refugee-art/
     assets/
       media/
         video1.mp4
         video2.mp4
   ```

2. **In your Google Sheet, use the file path:**
   | pid | title | video_url |
   |-----|-------|-----------|
   | video1 | My Video | /assets/media/video1.mp4 |

**Supported video formats:**
- `.mp4` (recommended - works everywhere)
- `.webm`
- `.ogg`

**Important:** For direct video files, you can also add a `thumbnail` column with a poster image (frame from the video or a custom image) that shows before the video plays.

---

## Part 2: Adding Audio

### Step 1: Prepare Your Audio Files

**Supported audio formats:**
- `.mp3` (recommended - works everywhere)
- `.ogg`
- `.wav`

### Step 2: Create Media Folder

Create a folder for your audio files:
```
syrian-refugee-art/
  assets/
    media/
      audio1.mp3
      audio2.mp3
      interview1.mp3
```

### Step 3: Add to Your Google Sheet

**Add an `audio_url` column:**

| pid | title | artist | audio_url | layout | collection |
|-----|-------|--------|-----------|--------|------------|
| audio1 | Refugee Story | Ahmed Ali | /assets/media/audio1.mp3 | syrian_refugee_art_item | syrian_refugee_art |
| audio2 | Traditional Music | Samira | /assets/media/audio2.mp3 | syrian_refugee_art_item | syrian_refugee_art |

### Step 4: Optional - Add Transcripts

**Add an `audio_transcript` column for accessibility:**

| pid | title | audio_url | audio_transcript |
|-----|-------|-----------|-----------------|
| audio1 | Interview | /assets/media/audio1.mp3 | This is the transcript of the interview... |

The transcript will appear as a collapsible section below the audio player.

---

## Part 3: Complete CSV Example

Here's how your Google Sheet should look with all media types:

| pid | title | artist | date | medium | video_url | audio_url | layout | collection | thumbnail | full | manifest |
|-----|-------|--------|------|--------|-----------|-----------|--------|------------|-----------|------|----------|
| artwork1 | Sunset Painting | Ahmed Ali | 2020 | Oil Painting | | | syrian_refugee_art_item | syrian_refugee_art | | | |
| video1 | Artist Interview | Ahmed Ali | 2020 | Video | https://youtube.com/watch?v=ABC123 | | syrian_refugee_art_item | syrian_refugee_art | | | |
| audio1 | Refugee Story | Samira | 2019 | Audio | | /assets/media/story1.mp3 | syrian_refugee_art_item | syrian_refugee_art | | | |

**Key points:**
- **Images:** Fill in `thumbnail`, `full`, and `manifest` columns
- **Videos:** Fill in `video_url` column (leave image columns empty)
- **Audio:** Fill in `audio_url` column (leave image and video columns empty)
- **All types:** Use the same `layout` and `collection` values

---

## Part 4: How It Works

### Priority Order

The system checks for media in this order:
1. **Video first** - If `video_url` exists, show video player
2. **Audio second** - If `audio_url` exists, show audio player  
3. **Image last** - Otherwise, show image viewer

**Example:**
- If you fill both `video_url` and `audio_url`, only video will show
- If you fill `video_url` and image columns, only video will show
- If you only fill image columns, image will show

### For Mixed Media

If you want to show both an image AND a video/audio:
- Use the image columns for the main display
- Add video/audio URLs in the metadata (they'll appear in the metadata table as links)

---

## Part 5: File Organization

### Recommended Folder Structure

```
syrian-refugee-art/
  _data/
    raw_images/
      syrian_refugee_art/     ← Images go here
        artwork1.jpg
        artwork2.jpg
  assets/
    media/                     ← Videos and audio go here
      video1.mp4
      video2.mp4
      audio1.mp3
      audio2.mp3
```

### File Naming

**Match your `pid` values:**
- If `pid: video1` → File: `video1.mp4`
- If `pid: audio1` → File: `audio1.mp3`
- If `pid: artwork1` → File: `artwork1.jpg`

---

## Part 6: Examples

### Example 1: YouTube Video

**Google Sheet:**
| pid | title | artist | video_url | layout | collection |
|-----|-------|--------|-----------|--------|------------|
| video1 | Documentary | Ahmed | https://www.youtube.com/watch?v=dQw4w9WgXcQ | syrian_refugee_art_item | syrian_refugee_art |

**Result:** Embedded YouTube player on the artwork page

### Example 2: Direct Video File

**Google Sheet:**
| pid | title | video_url | thumbnail |
|-----|-------|-----------|-----------|
| video1 | My Video | /assets/media/video1.mp4 | /assets/media/video1-poster.jpg |

**Files needed:**
- `assets/media/video1.mp4` (the video)
- `assets/media/video1-poster.jpg` (optional poster image)

**Result:** HTML5 video player with optional poster image

### Example 3: Audio with Transcript

**Google Sheet:**
| pid | title | audio_url | audio_transcript |
|-----|-------|-----------|-----------------|
| audio1 | Interview | /assets/media/interview.mp3 | This is the full transcript... |

**Files needed:**
- `assets/media/interview.mp3` (the audio file)

**Result:** Audio player with collapsible transcript below

---

## Part 7: Tips and Best Practices

### Video Tips

✅ **DO:**
- Use YouTube/Vimeo for easy hosting (no file size limits)
- Use MP4 format for direct files (best compatibility)
- Add poster images for direct video files (better user experience)
- Keep video files under 100MB if hosting yourself

❌ **DON'T:**
- Don't use spaces in filenames (use underscores)
- Don't upload huge video files directly (use YouTube/Vimeo instead)

### Audio Tips

✅ **DO:**
- Use MP3 format (best compatibility)
- Add transcripts for accessibility
- Keep audio files under 50MB
- Use descriptive filenames

❌ **DON'T:**
- Don't use spaces in filenames
- Don't forget to add transcripts for interviews/speech

### File Size Recommendations

- **Videos:** Under 100MB per file (or use YouTube/Vimeo)
- **Audio:** Under 50MB per file
- **Images:** Under 10MB per file

---

## Part 8: Troubleshooting

**Video not showing?**
- Check that `video_url` column is filled correctly
- For YouTube/Vimeo, make sure URL is complete
- For direct files, check file path starts with `/assets/media/`
- Make sure video file exists in the correct folder

**Audio not playing?**
- Check that `audio_url` column is filled correctly
- Verify file path starts with `/assets/media/`
- Make sure audio file exists
- Try MP3 format (most compatible)

**Both video and audio showing?**
- Only one will show (video takes priority)
- If you want both, use image + add audio as metadata link

**Transcript not appearing?**
- Make sure `audio_transcript` column is filled
- Check that there's content in the cell

---

## Quick Reference

| Media Type | Required Column | Example Value |
|------------|----------------|---------------|
| Image | `thumbnail`, `full` | `/img/derivatives/iiif/images/artwork1/full/250,/0/default.jpg` |
| YouTube Video | `video_url` | `https://www.youtube.com/watch?v=ABC123` |
| Vimeo Video | `video_url` | `https://vimeo.com/123456789` |
| Direct Video | `video_url` | `/assets/media/video1.mp4` |
| Audio | `audio_url` | `/assets/media/audio1.mp3` |
| Audio + Transcript | `audio_url`, `audio_transcript` | `/assets/media/audio1.mp3` + transcript text |

---

## Next Steps

1. Add `video_url` and/or `audio_url` columns to your Google Sheet
2. Fill in the URLs or file paths
3. Upload video/audio files to `assets/media/` folder (if using direct files)
4. Export your sheet as CSV
5. Run `bundle exec rake wax:pages syrian_refugee_art` to generate pages
6. Preview your site - videos and audio will appear automatically!

Need help? Just ask! 🎥🎵

