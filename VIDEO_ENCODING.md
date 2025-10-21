# Video Encoding Guide for ScrollyVideo

## Optimal FFmpeg Command

For the best ScrollyVideo experience, use this ffmpeg command to convert any video:

```bash
ffmpeg -i input.mp4 -c:v libx264 -preset medium -crf 25 -vf "scale='min(1280,iw)':'min(720,ih)':force_original_aspect_ratio=decrease" -g 30 -pix_fmt yuv420p -profile:v main -movflags +faststart -an output.mp4
```

## Command Breakdown

- **`-i input.mp4`** - Your source video file
- **`-c:v libx264`** - Use H.264 codec (best compatibility with WebCodecs)
- **`-preset medium`** - Good balance between encoding speed and compression
- **`-crf 25`** - Quality level (18-28 range: lower = better quality, 25 is optimal for web)
- **`-vf "scale='min(1280,iw)'..."`** - Smart scaling: downscales to 720p max but never upscales small videos
- **`-g 30`** - **CRITICAL**: Keyframe every 30 frames (~1 per second at 30fps) for smooth scrubbing
- **`-pix_fmt yuv420p`** - Maximum compatibility across browsers
- **`-profile:v main`** - H.264 Main profile for better compatibility
- **`-movflags +faststart`** - Optimize for web streaming (metadata at start)
- **`-an`** - Remove audio track (not needed for scroll videos)

## Alternative Resolutions

### 1080p (Higher Quality)
```bash
ffmpeg -i input.mp4 -c:v libx264 -preset medium -crf 24 -vf "scale='min(1920,iw)':'min(1080,ih)':force_original_aspect_ratio=decrease" -g 30 -pix_fmt yuv420p -profile:v main -movflags +faststart -an output.mp4
```

### 540p (Smaller File Size)
```bash
ffmpeg -i input.mp4 -c:v libx264 -preset medium -crf 27 -vf "scale='min(960,iw)':'min(540,ih)':force_original_aspect_ratio=decrease" -g 30 -pix_fmt yuv420p -profile:v main -movflags +faststart -an output.mp4
```

## Quality vs File Size Tuning

### Smaller File (Lower Quality)
Change `-crf 25` to `-crf 28` or `-crf 30`

### Higher Quality (Larger File)
Change `-crf 25` to `-crf 22` or `-crf 20`

### Faster Encoding
Change `-preset medium` to `-preset fast` or `-preset veryfast`

### Better Compression (Slower Encoding)
Change `-preset medium` to `-preset slower` or `-preset veryslow`

### Smoother Scrubbing (Larger File)
Change `-g 30` to `-g 15` (keyframe every 15 frames)

### Smaller File (May Skip Frames)
Change `-g 30` to `-g 60` (keyframe every 60 frames)

## Important Notes

1. **WebCodecs Optimization** - The `-g 30` setting provides smooth scrubbing with WebCodecs while keeping file sizes reasonable. WebCodecs efficiently decodes between keyframes, so you don't need `-g 1` (which creates massive files).

2. **File Size** - A 30-second 720p video will be ~2-5MB with these settings. Much smaller than all-keyframe encoding while maintaining smooth playback.

3. **Performance** - 720p is recommended for best balance between quality and performance. 1080p works but may impact performance on lower-end devices.

4. **Aspect Ratio** - The command maintains source aspect ratio and adds letterboxing if needed. For custom aspect ratios, adjust the scale values.

5. **GOP Size** - `-g 30` means keyframe every 30 frames. At 30fps, that's 1 keyframe per second. Adjust based on your needs.

## Testing Your Video

After encoding, test in the browser:
1. Place the video in `/demos/svelte/static/`
2. Update the src in `+page.svelte`: `src="{base}/your-video.mp4"`
3. Check that scrolling is smooth with no frame skipping

## Example

```bash
# Convert a 4K video to optimized 720p for ScrollyVideo
ffmpeg -i my-4k-video.mov -c:v libx264 -preset medium -crf 25 -vf "scale='min(1280,iw)':'min(720,ih)':force_original_aspect_ratio=decrease" -g 30 -pix_fmt yuv420p -profile:v main -movflags +faststart -an output.mp4
```

## Why This Command Works Well

1. **Smart Scaling** - `scale='min(1280,iw)'` only downscales if needed, never upscales or adds padding
2. **Small File Sizes** - `-crf 25` and `-preset medium` create compact files perfect for web
3. **Smooth Scrubbing** - `-g 30` balances file size and frame-seeking performance
4. **Web-Optimized** - `-movflags +faststart` enables progressive loading
5. **Universal Compatibility** - H.264 Main profile works everywhere

## Troubleshooting

**Video is choppy during scroll:**
- Try smaller GOP: change `-g 30` to `-g 15`
- Lower resolution (540p instead of 720p)
- Reduce `transitionSpeed` prop in ScrollyVideo component

**File size too large:**
- Increase `-crf` value (try 27 or 28)
- Use larger GOP: change `-g 30` to `-g 60`
- Use lower resolution
- Shorten video duration
- Use faster preset: `-preset medium` or `-preset fast`

**File size too small but quality is poor:**
- Decrease `-crf` value (try 23 or 22)
- Use higher resolution

**Video won't load:**
- Check codec is H.264 with `ffprobe output.mp4`
- Ensure `-pix_fmt yuv420p` was used
- Verify `-movflags +faststart` was applied
