# Reelo Video Lexicons

This directory provides video-related lexicons for Reelo, designed to remain compatible with Bluesky while supporting extended functionality such as:

- Video uploads of up to three minutes.
- Title fields (maximum of 200 characters).
- Hashtags for improved discovery and categorization.

---

## Files Overview

1. **`app.reelo.video.defs.json`**  
   - Includes the `jobStatus` schema, describing the state of a video processing job.

2. **`app.reelo.video.getJobStatus.json`**  
   - **Type**: `query`  
   - Retrieves the status of a specific video processing job by `jobId`.

3. **`app.reelo.video.getUploadLimits.json`**  
   - **Type**: `query`  
   - Reports user-specific video upload permissions and limits (e.g., maximum duration, daily quotas).

4. **`app.reelo.video.uploadVideo.json`**  
   - **Type**: `procedure`  
   - Accepts a `video/mp4` blob for processing on the Reelo PDS.  
   - Returns a `jobStatus` containing a `jobId`.

5. **`app.reelo.video.hashtag.json`**  
   - **Type**: `record`  
   - Describes a hashtag, including fields such as `tag`, `description`, and `usageCount`.

6. **`app.reelo.video.post.json`**  
   - **Type**: `record`  
   - Represents a fully published video post on Reelo. Key fields include:
     - **`videoBlob`**: Reference to the processed video file  
     - **`title`** (up to 200 characters)  
     - **`hashtags`**: Array of hashtag strings  
     - **`postedBy`**: Reference to the creator  
     - **`createdAt`**: Timestamp when the post was published

---

## Hashtags

- The `app.reelo.video.hashtag.json` file can store detailed data about each hashtag (e.g., usage count, description).  
- In `app.reelo.video.post.json`, `hashtags` is an array of strings. It can be cross-referenced with the hashtag records if there is a global database of hashtags.

---

## Cross-Posting to Bluesky

- When the uploaded video is **60 seconds or shorter**, it can be cross-posted more natively on Bluesky.  
- If the duration exceeds 60 seconds, Reelo can publish a simple text reference on Bluesky, for example:  
  *"Hey! Just posted a new video on Reelo: https://reelo.app/video/<videoURL>"*

This approach provides seamless interoperability while allowing longer videos to be hosted on Reelo.

---

## Example Flow

1. **Check Upload Limits**  
   Invoke `getUploadLimits` to verify if the user is allowed to upload videos and to confirm the maximum length (180 seconds).

2. **Upload Video**  
   Use `uploadVideo` with a `video/mp4` file. Receive a `jobStatus` object containing a `jobId`.

3. **Poll Job Status**  
   Call `getJobStatus` to track the progress of encoding or processing. Once `state == "JOB_STATE_COMPLETED"`, the final `blob` is ready.

4. **Post the Video**  
   Create a `app.reelo.video.post` record referencing the `videoBlob`. Provide a title (up to 200 characters) and an array of hashtags, then store or publish this record in the user repository or another feed system.

5. **(Optional) Cross-Post**  
   - If the video is 60 seconds or less, it can be embedded or attached directly in a Bluesky post.  
   - If it is longer, share a link to the Reelo page on Bluesky.

