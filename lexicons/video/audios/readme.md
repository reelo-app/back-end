# Reelo Audio Lexicons

This directory contains audio-related lexicons for use in Reelo videos. The schema is divided into **music** (licensed or curated) and **originals** (user-generated) audio, both of which reference a shared base definition.

---

## Files

### 1. `app.reelo.video.audios.defs.json`
A definitions file that includes `baseAudio`, covering:
- **`audioId`**: A unique identifier for the track  
- **`title`**: Display name or title of the audio  
- **`blob`**: A reference to the uploaded audio file (MP3, WAV, etc.)  
- **`duration`**: Audio length in seconds  
- **`addedBy`**: The user or account that added this track to Reelo  
- **`createdAt`**: Timestamp indicating when the audio record was created  
- **`usageCount`**: The number of times this track has been used in Reelo videos

### 2. `app.reelo.video.audios.music.json`
**Type**: `record`  
Represents **Music** sourced from Reelo’s official library, which may be licensed or curated. In addition to the fields in `baseAudio`, it includes:
- **`artistName`**, **`licenseType`**, **`coverArt`**, **`genre`**, **`label`**

### 3. `app.reelo.video.audios.originals.json`
**Type**: `record`  
Represents **Original** user-generated audio, such as voice recordings or other uploads. Beyond `baseAudio`, it contains:
- **`recordedBy`**, **`recordedAt`**, **`location`**

---

## Usage & Customization

- **Modular Structure**  
  Music and originals are kept separate for clarity, but both rely on the shared `baseAudio` definition.

- **Audio Formats**  
  Each record references a `blob` field, allowing MP3, WAV, or other formats to be stored or referenced.

- **Licensing & Ownership**  
  - `music.json` fields may include license terms for official tracks.  
  - `originals.json` can include additional attributes for privacy or ownership details.

- **Potential Queries & Procedures**  
  Adding procedures such as “uploadAudio” or “searchMusicLibrary” can create a more complete AT Protocol experience.

- **Integration with Reelo Videos**  
  When a user selects an audio track to accompany a video, the system may reference either a music record or an original audio record within the final video post schema.

