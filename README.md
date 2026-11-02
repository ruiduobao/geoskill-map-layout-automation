# Map Layout Automation (geoskill-map-layout-automation)

> Automate map layout with title, legend, scale bar and north arrow to PDF or PNG

---

## 1. Overview

Automatically lays out a raster map into a finished cartographic product: frame + title + legend (colorbar) + scale bar + north arrow, exported as high-resolution PNG and vector PDF. The scale bar length is derived from the frame width and reference latitude as a round number of kilometers on the 1-2-5 sequence; the north arrow is a standard north-pointing arrow.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-map-layout-automation.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `layout.png` | PNG | Laid-out map (primary output) |
| `layout.pdf` | PDF | Vector version |
| `layout_data.tif` | GeoTIFF | Data raster (verifiable output) |
| `layout_meta.json` | JSON | Scale bar / element toggles / dpi |

Each run also produces `output-manifest.json` (run manifest).


## 6. Technical Principle

meters_per_degree_lon=111320·cos(lat) → scale_bar_km=round(frame width×fraction) → draw_scale_bar / north_arrow data-coordinate decorations → matplotlib layout.

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
