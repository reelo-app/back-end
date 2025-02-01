# Reelo Comments Lexicons

This folder contains schemas for comments, replies, and likes on comments or replies within Reelo. The structure is split into multiple files for clarity and modularity.

---

## File Overview

1. **`app.reelo.comments.defs.json`**  
   Provides shared definitions, including:
   - `moderationStatus`: An enum representing a comment or reply's moderation state.  
   - `subjectReference`: A generic reference to the record being commented on.

2. **`app.reelo.comments.comment.json`**  
   **Type**: `record`  
   Represents a **top-level comment** on a subject (video, post, etc.).  
   - Key fields include `subject`, `commentedBy`, `text`, `createdAt`, and `moderationStatus`.

3. **`app.reelo.comments.reply.json`**  
   **Type**: `record`  
   Represents a **reply** directed at a comment (or potentially another reply if the schema is adjusted).  
   - Key fields include `commentUri`, `repliedBy`, `text`, `createdAt`, and `moderationStatus`.

4. **`app.reelo.comments.like.json`**  
   **Type**: `record`  
   Describes a “like” applied to a comment or reply.  
   - Uses `subject` referencing `app.reelo.comments.defs#subjectReference` to identify the record being liked.

---

## Usage & Customization

- **Subject References**  
  The `subjectReference` mechanism allows comments to be attached to any record in the system (such as a video or post) by including the appropriate URI in `comment.subject`.
- **Counters**  
  Fields like `likeCount` or `replyCount` may reside in the comment or reply records and require updates whenever a new like or reply is created or removed.
- **Reply Nesting**  
  Additional nesting can be achieved by introducing a `parentUri` field in `reply.json` that points to another reply record, enabling deeper threading.

---

## Example Flow

1. **Posting a Comment**  
   A user posts a comment on a video by creating a `app.reelo.comments.comment` record, specifying the video’s URI in `subject.uri`, the user in `commentedBy`, and the message text in `text`.

2. **Replying to a Comment**  
   Another user replies by creating a `app.reelo.comments.reply` record, setting `commentUri` to the original comment’s URI.

3. **Adding a Like**  
   A like is added by creating a `app.reelo.comments.like` record, referencing either the comment or reply through `subject.uri`.

4. **Counter Updates**  
   If counters are maintained in the comment or reply records (for likes or reply counts), these may be incremented whenever a corresponding interaction occurs.

