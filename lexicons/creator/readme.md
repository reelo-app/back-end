# Reelo Creator Lexicons

This folder contains lexicon schemas related to user accounts (creators) within Reelo. The aim is to maintain **full interoperability** with Bluesky actors, allowing Bluesky users to log in on Reelo with their existing DID/handle and enabling Reelo users to appear seamlessly in Bluesky.

---

## Files

### 1. `app.reelo.creator.defs.json`
A definitions file containing reusable sub-schemas:

- **`moderationStatus`**  
  An enum with values like `["active", "banned", "silenced", "adult"]` to represent an account’s moderation state.

- **`accountReference`**  
  An object requiring `did` (string, format: `did`) and `handle` (string, format: `handle`).  
  Used as a standardized way to reference a user.

### 2. `app.reelo.creator.profile.json`
A **record** representing a user profile in Reelo. Key fields include:

- **`did`** (string, format: `did`): A user’s decentralized identifier.  
- **`handle`** (string, format: `handle`): A username/handle such as `user.reelo.app` or `someone.bsky.social`.  
- **`displayName`**, **`description`**, **`avatar`**, **`banner`**: Profile fields similar to those in Bluesky.  
- **`moderationStatus`** (ref to `app.reelo.creator.defs#moderationStatus`): Indicates the user’s state (active, banned, silenced, adult).  
- **`indexedAt`** and **`createdAt`**: Timestamps for indexing and creation.  
- **`viewer`**: A reference to `app.bsky.actor.defs#viewerState`, which provides Bluesky-compatible relationship data (follow, mute, block, etc.).  
- **`labels`**: An array referencing `com.atproto.label.defs#label`, used in the Bluesky labeling system.

> **Note**: This profile record is considered **public**. Information such as password hashes, email verification, and similar sensitive details should be kept in other records or within private backend systems.

---

## Usage & Compatibility

1. **Bluesky Interoperability**  
   The use of `did` and `handle` in formats aligned with `app.bsky.actor.profile` allows standard Bluesky accounts to function within Reelo. The `viewer` reference ties into Bluesky's standard for follower, mute, and block relationships.

2. **Extending vs. Duplicating Fields**  
   Since the Lexicon specification does not include a direct “extends” mechanism, Reelo replicates key fields from `app.bsky.actor.profile`. This method preserves structure and ensures recognizable data within typical Bluesky environments.

3. **Data Privacy**  
   Fields in the public profile should remain non-sensitive. Extra private data—such as authentication tokens, emails, or 2FA configuration—belongs in a secure, non-public location.

4. **Further Development**  
   Additional user states, roles, or preferences may be placed in `app.reelo.creator.defs.json`. Custom endpoints for processes like account creation or login can be implemented outside these public records, according to application requirements.