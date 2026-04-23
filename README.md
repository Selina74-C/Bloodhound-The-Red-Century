# Bloodhound: The Red Century

Official media repository for the video presentation of **Bloodhound: The Red Century**.

## Quick Links

- 🎬 [Watch / Download Official Video](eddd4c1025ffe2dd5121718e1ebcb3b2.mp4)
- 🧩 Premiere Project: `Gio AIGC.prproj`
- 🛠 ComfyUI Workflow: [`workflows/bloodhound_red_century_workflow.json`](workflows/bloodhound_red_century_workflow.json)

## Featured Media

- **Official Video File:** `eddd4c1025ffe2dd5121718e1ebcb3b2.mp4`
- **Format:** `.mp4`

## Repository Structure

- `eddd4c1025ffe2dd5121718e1ebcb3b2.mp4` — Final rendered video
- `Gio AIGC.prproj` — Adobe Premiere project source
- `assets/images/` — Thumbnail and preview images for documentation
- `assets/video/` — Optional folder for additional clips or alternate exports
- `assets/reference_images/` — Six source reference images (`image1.png` … `image6.png`) that drive the ComfyUI workflow
- `workflows/bloodhound_red_century_workflow.json` — ComfyUI workflow that reconstructs the video as a 10-shot Nano Banana 2 → Veo 3.1 pipeline

## Thumbnail Preview for GitHub (Optional)

If you want a professional visual preview in `README.md`, add:

- `assets/images/video-frame.jpg`

Then include this snippet:

```md
[![Bloodhound: The Red Century — Video Preview](assets/images/video-frame.jpg)](eddd4c1025ffe2dd5121718e1ebcb3b2.mp4)
```

## ComfyUI Workflow — Usage

The workflow at [`workflows/bloodhound_red_century_workflow.json`](workflows/bloodhound_red_century_workflow.json) reconstructs the film as 10 representative shots using a **Nano Banana 2 (keyframe T2I)** → **Veo 3.1 (8-second I2V)** pipeline, grouped into three acts:

- **Act I — Establishing** (S01–S03): wide desert, crow on skull, crane pullback. Uses `image1.png`, `image2.png`, `image3.jpeg` as shared refs.
- **Act II — Pursuit & Crash** (S04–S09): driver gear-shift close-up, raider binoculars, gang loading weapons, rear-view mirror, Cadillac STS T-bone, Mustang rollover. Uses `image4.png` (driver POV) and `image5.png` (raider Cadillac STS 2004).
- **Act III — Biopunk Finale** (S10): the wounded protagonist finds the blood-vined red Buick Century in the abandoned factory. Uses `image6.png`.

### 1. Prerequisites

- ComfyUI updated to a build that ships the **Nano Banana 2** and **Veo 3 / 3.1** partner nodes (ComfyUI Desktop stable ≥ the October 2025 partner-nodes release, or the latest nightly).
- A logged-in ComfyUI account (or an API Key configured in Settings) with credits for the Google API nodes. See the [API Nodes overview](https://docs.comfy.org/tutorials/partner-nodes/overview).
- A secure network environment that the API nodes accept (`127.0.0.1` / `localhost`, an `https://` host, or API-Key login on a LAN).

### 2. Install the reference images

Copy the six source images from `assets/reference_images/` into your ComfyUI input folder:

```bash
cp assets/reference_images/image*.{png,jpeg} /path/to/ComfyUI/input/
```

The `LoadImage` nodes in the workflow reference exactly these filenames:

- `image1.png`, `image2.png`, `image3.jpeg` — shared establishing shots (fed into S01 + S03 via `BatchImagesNode`)
- `image4.png` — driver interior POV (S04)
- `image5.png` — raider Cadillac STS 2004 (S08)
- `image6.png` — blood-vined Buick Century (S10)

### 3. Load and run the workflow

1. In ComfyUI, use Workflow → Open** and select `workflows/bloodhound_red_century_workflow.json`.
2. Read the red “Setup — read first”** note in the top-left corner of the canvas.
3. Queue the graph. The Nano Banana 2 nodes will render 10 keyframe stills; the Veo 3.1 nodes will then render ten 8-second clips with audio.
4. If your ComfyUI build does not list the exact model id `veo-3.1-generate-preview`, reselect the nearest Veo 3.1 entry on each of the 10 Veo nodes (e.g. `veo-3.1-fast-generate-preview`); `veo-3.0-fast-generate-001` works as a fallback.

### 4. Outputs

- `ComfyUI/output/keyframes/Bloodhound_S01_wide_desert…*.png` — 10 archived keyframes
- `ComfyUI/output/video/Bloodhound_S01_wide_desert.mp4` … `Bloodhound_S10_biopunk_finale.mp4` — 10 individual 8-second clips

### 5. Final Cut

Import all 10 clips into a Premiere / Resolve sequence in `S01 → S10` order. The source film relies on short-cut pacing (3–5 seconds per shot), handheld-style cuts, overlaid engine roars / gunfire / ambient red-factory SFX, and the Mad-Max-flavored color grade. The companion project file `Gio AIGC.prproj` mirrors this edit structure.

## Publishing Notes

- GitHub may not autoplay local `.mp4` files inline in all views; a thumbnail + link provides the most consistent result.
- Keep the current video filename unchanged unless you also update links in `README.md`.
