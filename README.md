## 🎬 ia-search

**ia-search** is an interactive terminal browser and downloader for the **Internet Archive**, powered by `fzf` and `ia-cli`.  
It lets you **browse**, **search**, **play**, and **download** media directly from your terminal — no web browser needed.

Now features a **Smart Launch Monitor** that intelligently manages the transition between the terminal and your media player.

---

## 🖼️ Screenshots

<img width="1276" height="998" alt="Screenshot from 2025-11-02 20-58-55" src="https://github.com/user-attachments/assets/cacb3f1e-aac3-4214-a8a2-031470428da8" />
<p align="center"><i>🏁 Main menu showing cached top collections</i></p>

<img width="1180" height="974" alt="Screenshot from 2025-11-02 21-06-32" src="https://github.com/user-attachments/assets/e5881379-b20f-466b-a5cb-8e828cc5bb2e" />
<p align="center"><i>🔍 Searching across all Internet Archive collections</i></p>

<img width="1180" height="974" alt="Screenshot from 2025-11-02 21-07-18" src="https://github.com/user-attachments/assets/9846adb8-98fb-4e47-a9f1-0a5f616803ac" />
<p align="center"><i>🎥 Selecting an item result with fuzzy finder</i></p>

<img width="1180" height="974" alt="Screenshot from 2025-11-02 21-09-37" src="https://github.com/user-attachments/assets/f0d4bf5c-2cce-459a-be77-7aa4ce7d5954" />
<p align="center"><i>📂 Browsing files within a selected Internet Archive item</i></p>

<img width="1180" height="974" alt="Screenshot from 2025-11-02 21-10-06" src="https://github.com/user-attachments/assets/5debd339-c35d-4d16-a929-57482059d4c0" />
<p align="center"><i>🎬 Choosing to play or download the file</i></p>

---

## ✨ Features

- 🧭 **Interactive collection browser** with pagination & local cache  
- 🚀 **Smart Launch Monitor** — Automatically detects when `mpv` has successfully initialized video/audio before returning to the menu (prevents premature switching).
- 🛡️ **Robust Filename Support** — Safely handles complex filenames (e.g., Anime release groups with `[]`, `()` symbols).
- 🔍 **Search across all collections** with fuzzy finder (`fzf`)  
- 🎥 **Play videos** & 🎧 **listen to audio** with `mpv`  
- 🖼️ **View images** instantly using `nsxiv`  
- 📄 **Open PDFs** seamlessly with `zathura`  
- ⬇️ **Download** any file directly from Internet Archive  
- 💬 **Subtitle auto-detection** for `.srt` / `.ass` files  
- 🧹 **Temp cleanup** after image/PDF viewing  

---

## ⚙️ Dependencies

| Tool | Purpose |
|------|----------|
| [`ia`](https://archive.org/services/docs/api/internetarchive/cli.html) | Internet Archive CLI (Core search/list) |
| [`fzf`](https://github.com/junegunn/fzf) | Fuzzy finder UI |
| [`jq`](https://jqlang.github.io/jq/) | Parsing API JSON responses |
| [`mpv`](https://mpv.io/) | Video & audio player |
| [`nsxiv`](https://github.com/nsxiv/nsxiv) | Image viewer |
| [`zathura`](https://pwmt.org/projects/zathura/) | PDF viewer |
| [`yt-dlp`](https://github.com/yt-dlp/yt-dlp) | Downloader for videos |
| [`curl`](https://curl.se/) | File downloader / API fetcher |
| [`pv`](https://www.ivarch.com/programs/pv.shtml) | Progress bar for launch monitoring |

### 🧩 Optional Viewer Config

You can replace defaults easily in the script variables:
```bash
VIDEO_PLAYER="mpv"
AUDIO_PLAYER="mpv"
IMAGE_VIEWER="nsxiv"
PDF_VIEWER="zathura"
VIDEO_DOWNLOADER="yt-dlp"
````

-----

## 🔧 Installation

1.  Clone the repository:

    ```bash
    git clone [https://github.com/ahloiscreamo/ia-search.git](https://github.com/ahloiscreamo/ia-search.git)
    cd ia-search
    ```

2.  Make it executable:

    ```bash
    chmod +x ia-search
    ```

3.  (Optional) Move it to your `$PATH`:

    ```bash
    sudo mv ia-search /usr/local/bin/
    ```

4.  Run it:

    ```bash
    ia-search
    ```

-----

## 🧭 Navigation Overview

```
📚 Top Collections (cached)
 ├── [🔍 Search all collections]
 ├── [🔄 Refresh cache]
 ├── [➡️ Next page]
 └── [❌ Exit]
```

### 🔍 Search Mode

  * Type a query → see instant results
  * Press `ESC` → return to query input
  * Press `ESC` again → return to main collections

### 🚀 Smart Launch Behavior

When you select a video to play, the script pauses the interface and monitors `mpv`'s internal logs. It will only return you to the search list once it confirms the video window is actually open (`VO:`) or audio is playing (`AO:`).

-----

## 🧠 Example Queries

Search for Japanese movies:

```bash
mediatype:movies AND language:japanese
```

Public domain audio:

```bash
mediatype:audio AND subject:publicdomain
```

Scanned art books:

```bash
mediatype:image AND subject:art
```

Animation PDFs:

```bash
mediatype:texts AND subject:animation
```

-----

## 📜 Common Search Fields

| Field        | Example                 | Description               |
| ------------ | ----------------------- | ------------------------- |
| `mediatype`  | `mediatype:movies`      | Type of content           |
| `title`      | `title:"Studio Ghibli"` | Search by title           |
| `creator`    | `creator:"NHK"`         | Filter by uploader/author |
| `subject`    | `subject:japan`         | Filter by tags            |
| `language`   | `language:japanese`     | Filter by language        |
| `year`       | `year:1990`             | Filter by year            |
| `collection` | `collection:anime`      | Specific IA collection    |

-----

## 🧰 Example Flow

```
📚 Loading collections from cache...
🔍 Type search query (ESC to return to main) > mediatype:movies AND subject:japan
🔎 Searching for "mediatype:movies AND subject:japan" ...
📂 Fetching file list for: tokyo-streets-1990 ...
🎬 Choose action for file > ▶️ Play
🎞️ Playing video...
🚀 Launching mpv: 0:00:02 [========>                      ]
(Returns to menu only after player confirms launch)
```

-----
