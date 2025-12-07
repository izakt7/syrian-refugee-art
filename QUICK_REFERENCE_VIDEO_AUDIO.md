# Quick Reference: Video & Audio

## Adding Videos

### YouTube/Vimeo (Easiest)
**In your Google Sheet:**
- Add column: `video_url`
- Fill with: `https://www.youtube.com/watch?v=VIDEO_ID` or `https://vimeo.com/VIDEO_ID`

### Direct Video Files
1. Put video file in: `assets/media/video1.mp4`
2. In Google Sheet: `video_url` = `/assets/media/video1.mp4`
3. Optional: Add `thumbnail` for poster image

---

## Adding Audio

1. Put audio file in: `assets/media/audio1.mp3`
2. In Google Sheet: 
   - Add column: `audio_url` = `/assets/media/audio1.mp3`
   - Optional: Add column: `audio_transcript` = "Transcript text here"

---

## Your Google Sheet Columns

**Required for all:**
- `pid`, `title`, `layout`, `collection`

**For images:**
- `thumbnail`, `full`, `manifest`

**For videos:**
- `video_url` (YouTube/Vimeo URL or file path)

**For audio:**
- `audio_url` (file path)
- `audio_transcript` (optional)

---

## Priority Order

1. Video (if `video_url` filled) → Shows video player
2. Audio (if `audio_url` filled) → Shows audio player  
3. Image (if image columns filled) → Shows image viewer

**Only one will display** - video takes priority over audio, audio takes priority over image.

---

## File Formats

**Videos:** `.mp4` (best), `.webm`, `.ogg`
**Audio:** `.mp3` (best), `.ogg`, `.wav`

---

## Examples

### YouTube Video
```
pid: video1
title: Artist Interview
video_url: https://www.youtube.com/watch?v=ABC123
```

### Direct Video File
```
pid: video1
title: My Video
video_url: /assets/media/video1.mp4
thumbnail: /assets/media/video1-poster.jpg
```

### Audio with Transcript
```
pid: audio1
title: Refugee Story
audio_url: /assets/media/story1.mp3
audio_transcript: This is the full transcript...
```

---

## Need More Help?

See `VIDEO_AUDIO_GUIDE.md` for complete instructions!

