# Reelo Actions Lexicons

This directory contains record definitions in the AT Protocol style for user actions within Reelo. The following actions are included:

1. **Follow** (`app.reelo.actions.follow`)  
2. **Block** (`app.reelo.actions.block`)  
3. **Report** (`app.reelo.actions.report`)  

Each record stores structured data about its respective action. More details on these records are provided below.

---

## Files

### 1. `app.reelo.actions.follow.json`
**Type**: `record`  
Represents an action where one user (`follower`) follows another (`followed`).  
- **`mutual`** indicates whether the followed user also follows the follower.

### 2. `app.reelo.actions.block.json`
**Type**: `record`  
Captures a scenario where one user (`blocker`) blocks another (`blocked`).

### 3. `app.reelo.actions.report.json`
**Type**: `record`  
Describes a report action, where a user (`reportedBy`) files a report against another user or a piece of content (`subjectUri`).  
- **`reason`** contains a category or label (spam, harassment, etc.).  
- **`details`** may include additional information.

---

## Usage & Customization

- **User References**  
  Each record references `app.reelo.creator.defs#accountReference` to identify the user(s) involved.
- **Time Stamps**  
  The `createdAt` property indicates when the action was performed.
- **Extensions**  
  It is possible to include fields for scenarios like pending follow requests, automatic comment blocking upon a user block, or an expanded list of report reasons.

---

## Integration with Other Modules

- **Following**  
  The profile or social graph layer can reflect `follow` records to update follower/following counts or relationships.
- **Blocking**  
  The application logic can interpret `block` records to limit or prevent certain interactions.
- **Reporting**  
  Moderation systems or administrative tools can analyze `report` records to address flagged content or behavior.