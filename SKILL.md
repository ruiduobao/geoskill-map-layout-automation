---
name: geoskill-map-layout-automation
description: 'Automate map layout with title, legend, scale bar and north arrow to PDF or PNG'
---

# 地图排版自动化 | Map Layout Automation

Automatically lay out a raster map into a finished cartographic product: map frame + title + legend (colorbar) + scale bar + north arrow, output as high-resolution PNG and vector PDF.

The scale bar length is converted from the map-frame width and the reference latitude into an integer number of kilometers following a 1-2-5 sequence; the north arrow is a standard north-pointing arrow.

## Core Algorithm / 核心算法

meters_per_degree_lon=111320·cos(lat) → scale_bar_km=round(map_width×fraction) → draw_scale_bar/north_arrow data-coordinate decoration → matplotlib layout.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## Usage / 使用方法

### Example 1 (synthetic data, offline)

```bash
python geoskill-map-layout-automation.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2 (custom title and color scheme)

```bash
python geoskill-map-layout-automation.py --input dem.tif --title "terrain of the study area" --cmap viridis
```

### Example 3 (omit the north arrow)

```bash
python geoskill-map-layout-automation.py --input dem.tif --no-north
```

### Example 4 (adjust the scale bar fraction)

```bash
python geoskill-map-layout-automation.py --input dem.tif --bar-fraction 0.35
```

### Example 5 (high-dpi output)

```bash
python geoskill-map-layout-automation.py --input dem.tif --dpi 200
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `layout.png` | PNG | Layout map (main deliverable) |
| `layout.pdf` | PDF | Vector version |
| `layout_data.tif` | GeoTIFF | Data raster (verifiable deliverable) |
| `layout_meta.json` | JSON | Scale bar/element toggles/dpi |

Each run also produces `output-manifest.json` (run manifest).

## Data Source / 数据源 / Source

Local GeoTIFF / vector files; `--synthetic` mode generates physically consistent simulated data, fully offline.

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is performed locally; no user data is uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
