# Reelo Feed Lexicons

This folder provides queries (and optional records) for managing and retrieving feed data in Reelo. The queries include:

- **Home Timeline**: Videos from followed users.
- **Trending Videos**: Popular or high-engagement videos.
- **Unified Feed**: A single advanced query with filtering options for hashtags, keywords, user lists, and more.
- Additional specialized feeds (by hashtag, keyword, etc.) defined elsewhere.

---

## File Overview

1. **`app.reelo.feed.defs.json`**  
   Contains shared definitions such as `feedItem`, which represents an individual feed entry. This item typically references the Reelo video record (`app.reelo.video.post`) along with associated metadata (URIs, labels, etc.).

2. **`app.reelo.feed.getHomeTimeline.json`**  
   **Type**: `query`  
   Returns a feed of videos posted by accounts followed by the authenticated user.  
   - **Parameters**: `limit`, `cursor`, `sort`  
   - **Response**: An array of `feedItem` objects plus a `cursor` for pagination.

3. **`app.reelo.feed.getTrendingVideos.json`**  
   **Type**: `query`  
   Retrieves trending videos based on engagement metrics (like counts, share counts, etc.).  
   - **Parameters**: `limit`, `cursor`, `region`, `timeRange`  
   - **Response**: An array of `feedItem` objects plus a `cursor`.

4. **`app.reelo.feed.getUnifiedFeed.json`**  
   **Type**: `query`  
   Offers a single query that supports multiple filters, including `hashtags[]`, `keywords[]`, `userDids[]`, and `minLikes`.  
   - **Parameters**: `limit`, `cursor`, `sort`, plus optional filters  
   - **Response**: An array of `feedItem` objects plus a `cursor`.

5. **Additional Queries**  
   - **`app.reelo.feed.getVideosByHashtag.json`**  
   - **`app.reelo.feed.getVideosByKeyword.json`**  
   - **`app.reelo.feed.generator.json`** (optional) for creating a Bluesky-compatible custom feed.

---

## Usage

### Home Timeline
The service gathers recent videos from accounts that the authenticated user follows. Sorting may be chronological or based on an algorithmic ranking.

### Trending Videos
Videos with higher engagement metrics (views, likes, shares, etc.) over a specific time frame appear as trending.

### Unified Feed
Accepts a variety of filters and sorting options in one request. Useful when a single, flexible endpoint is preferable to multiple narrower queries.

---

## Implementation Details

Each query uses parameters and a cursor mechanism to support pagination. The system typically stores video data in a database or index for efficient filtering and sorting. The response follows the defined schema, returning an array of `feedItem` objects and a `cursor` when additional pages are available.

---

## TO-DO

- Additional queries such as `getVideosByLocation` or `getVideosForYou` can be included.  
- Labels and moderation can be integrated by attaching `com.atproto.label.defs#label` to each `feedItem`, allowing the feed to apply warnings or filtering for sensitive content.

