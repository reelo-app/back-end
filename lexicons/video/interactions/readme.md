# Reelo Video Interactions Lexicons

This folder provides **record definitions** for user interactions on Reelo videos, following a modular, AT Protocol–inspired approach. The defined interactions include comments, replies, likes, shares, and reports.

---

## Files

1. **`app.reelo.video.interactions.defs.json`**  
   Shared definitions containing:
   - **`moderationStatus`**: An enum capturing moderation states (`active`, `removed`, `silenced`, etc.).  
   - **`subjectReference`**: A generic reference (URI/CID) pointing to the item being interacted with (e.g., a video or comment).

2. **`app.reelo.video.interactions.comment.json`**  
   **Type**: `record`  
   Describes a top-level comment on a Reelo video (usually references a `videoUri` from `app.reelo.video.post`). Tracks user information, content, timestamps, moderation status, and counters like likes or replies.

3. **`app.reelo.video.interactions.reply.json`**  
   **Type**: `record`  
   Represents a reply to a comment (or potentially another reply). Fields typically include the author, text, timestamps, moderation status, and like counts.

4. **`app.reelo.video.interactions.like.json`**  
   **Type**: `record`  
   A “like” that may target any record (video, comment, or reply). Relies on `subject`, referencing `app.reelo.video.interactions.defs#subjectReference` to identify the object being liked.

5. **`app.reelo.video.interactions.share.json`**  
   **Type**: `record`  
   Depicts a “share” action that usually references a video, though it can also point to a comment or reply. Supports a `destination` field (e.g., “Bluesky”, “copyLink”) to indicate the sharing platform or method.

6. **`app.reelo.video.interactions.report.json`**  
   **Type**: `record`  
   Records a user “report” for inappropriate or rule-violating content. References a subject (video, comment, reply, or user) and includes a reason, optional details, and timestamps.

---

## Usage and Customization

- **Schema Enhancements**  
  It is possible to enrich the current records with additional fields (e.g., images, pinned replies, or nested-level indicators for thread depth).
- **Moderation**  
  The `moderationStatus` can be updated by an automated process or by moderators.
- **Counters**  
  Fields such as `likeCount` or `replyCount` may be stored in the relevant records and updated dynamically or on-demand.

---

## Interoperability with Bluesky

- **Protocol Alignment**  
  The structure of these records (and the use of references) follows the AT Protocol style, facilitating smooth interaction with Bluesky or similar ecosystems.
- **Idea: Cross-Protocol Interactions**  
  Developers can implement specific procedures (e.g., “like via Bluesky”) referencing `app.bsky.feed.post` or rely on the existing `subjectReference` pattern for universal linking.