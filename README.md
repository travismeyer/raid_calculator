# Array Capacity Calculator

A self-contained, dark-mode RAID and ZFS capacity calculator. Enter your drive count and size, pick a layout, and get live usable capacity, redundancy overhead, filesystem overhead, fault tolerance, and a visual breakdown of exactly where data and parity live on the array.

No build step, no dependencies to install, no backend — it's a single HTML file plus a handful of icon assets.

---

## Features

* **15 layouts** across Standard RAID (JBOD, 0, 1, 5, 6, 10, 50, 60) and ZFS (Stripe, Mirror, Striped Mirrors, RAIDZ1, RAIDZ2, RAIDZ3)
* **Multi-vdev / multi-group support** for RAID 50, RAID 60, Striped Mirrors, and RAIDZ1–3, with validation on drive-per-group minimums
* **Hot spare modeling** — spares are tracked separately from the array and shown as reserved, non-usable capacity
* **Decimal vs. binary display toggle** (TB/GB as advertised vs. TiB/GiB as most OSes report)
* **Filesystem overhead estimates** for NTFS, ReFS, exFAT, FAT32, ext4, XFS, ZFS native, and APFS
* **Live Array Visualizer** — renders the actual stripe/parity/mirror layout per vdev, with a colorblind-safe cyan/orange palette (pattern-differentiated, not color-only) and a distinct marker for hot spares
* **Reset button** to clear the form and start over
* Fully responsive, keyboard-accessible, and respects `prefers-reduced-motion`

---

## File Structure

```
/
├── index.html                    Entire app — HTML, CSS, and JS in one file
└── assets/
    └── images/
        ├── favicon.svg            Primary icon (modern browsers)
        ├── favicon.ico            Multi-res fallback (16/32/48)
        ├── favicon-16.png
        ├── favicon-32.png
        ├── favicon-48.png
        └── favicon-180.png        Apple touch icon
```

Keep this structure intact — `index.html` references the icons at `assets/images/...`, so both need to stay in the repo together at those relative paths.

---

## Running Locally

Just open `index.html` directly in a browser, or serve the folder with any static file server, e.g.:

```
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

---

## Customizing

* **Colors** — all theme colors are CSS custom properties in the `:root` block at the top of the `<style>` section (`--accent-cyan`, `--accent-orange`, `--accent-purple`, `--accent-green`, etc.).
* **RAID/ZFS levels** — defined in the `RAID_LEVELS` object in the `<script>` section. Each entry defines minimum drives, the usable-capacity formula, fault-tolerance description, and visualizer behavior — add a new key there to add a layout.
* **Filesystem overhead values** — defined in the `FILESYSTEMS` object, as approximate percentages with a short note per format.

---

## Notes on Accuracy

Filesystem overhead percentages are industry-typical approximations and will vary by allocation unit size, reserved-block configuration, and vendor implementation — they're meant to give a realistic ballpark, not an exact figure for a specific deployment. RAID/ZFS capacity math itself follows standard formulas and is exact given the inputs provided.

---

## License

See License File
