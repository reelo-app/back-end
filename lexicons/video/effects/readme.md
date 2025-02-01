# Reelo Video Effects Lexicons

This directory defines modular schemas for various Reelo video effects, grouped by category:

- **AI**: AI-driven effects (e.g., background removal, style transfer).  
- **AR**: Augmented reality components (3D face masks, plane tracking).  
- **Filters**: Standard LUT-based or color manipulation filters.  
- **Overlays**: Stickers, frames, and other visual elements.  
- **Interactives**: Game-like or user-interactive effects.

---

## Files

1. **`app.reelo.video.effects.defs.json`**  
   A definitions file that introduces `baseEffect`, holding:
   - **`effectId`**, **`name`**, **`description`**, **`creator`**, **`createdAt`**, **`usageCount`**

2. **`app.reelo.video.effects.ai.json`**  
   **Type**: `record`  
   AI-based effects that reference `baseEffect` plus:
   - **`modelName`**, **`modelVersion`**, **`aiType`**

3. **`app.reelo.video.effects.ar.json`**  
   **Type**: `record`  
   AR-based effects that reference `baseEffect` plus:
   - **`arModel`** (3D asset), **`trackingType`**, **`supportsMultipleFaces`**

4. **`app.reelo.video.effects.filters.json`**  
   **Type**: `record`  
   Standard filters that reference `baseEffect` plus:
   - **`filterFile`** (blob), **`intensity`** (0–1)

5. **`app.reelo.video.effects.overlays.json`**  
   **Type**: `record`  
   Overlays like stickers or frames that reference `baseEffect` plus:
   - **`overlayBlob`**, **`position`**, **`scalable`**, **`animated`**

6. **`app.reelo.video.effects.interactives.json`**  
   **Type**: `record`  
   Interactive, game-like effects that reference `baseEffect` plus:
   - **`scriptBlob`**, **`interactionType`**, **`scoresEnabled`**, **`multiplayer`**

---

## Usage & Compatibility

- **Modular Design**  
  Each effect type exists as a separate record while sharing fields from `baseEffect`. This approach aligns with the AT Protocol’s preference for references and individual JSON files.

- **Interchangeability**  
  Because each record uses a similar structure, it is possible to aggregate and display effects across multiple categories within a single interface or feed.

- **TO-DO**  
  - **Queries & Procedures**: Implement methods to list or search for effects.  
  - **Licensing & Submissions**: Add fields for AI/AR licensing details or user-generated submissions (e.g., custom scripts).  
  - **Enhanced Functionality**: Track usage data and integrate advanced moderation or rating systems as needed.

