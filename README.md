# Sushi Eve — AR Menu (MindAR Image Tracking)

## Folder structure
```
project/
├── index.html
├── css/
│   └── style.css
├── js/
│   ├── app.js                    main app logic
│   └── lib/
│       ├── mindar-image-three.js  MindAR core (image tracking)
│       ├── controller-mGt1s8dJ.js MindAR dependency chunk
│       └── ui-fBadYuor.js         MindAR dependency chunk
├── models/
│   ├── sushi.glb
│   ├── ramen.glb
│   ├── burger.glb
│   ├── dimsum.glb
│   └── cake.glb
├── marker/
│   ├── marker.png      print this / display it — the physical marker
│   └── targets.mind     compiled image-target data MindAR matches against
└── README.md
```

## How to run it
```
cd project
python3 -m http.server 8000      (or: py -m http.server 8000  on Windows)
```
Open `http://localhost:8000` in your browser and allow camera access.

Note: this now needs an internet connection even when running locally —
`three.js` itself is loaded from unpkg.com via an import map (only the MindAR
library and your models are local). If you need a fully offline version,
say so and I'll download and vendor three.js locally too.

## How tracking works now
This uses **real image tracking** (MindAR), not a generic shape detector:
- `marker/targets.mind` was compiled specifically from your `marker.png`
  using MindAR's feature-matching pipeline.
- The camera feed is matched against those exact features, so it will only
  lock onto your specific marker — not any other dark/square object.
- MindAR also gives full 6-DOF pose, so the 3D model now skews in proper
  perspective as you move the camera around the marker.

## Gestures
- Drag: rotate the dish
- Pinch (or scroll wheel on desktop): zoom
- Fast horizontal swipe: switch to next/previous dish

## Customizing
- Dish order/names/models: edit the `DISHES` array at the top of `js/app.js`.
- Nutrition/description/price info panels are the next build step — not
  included in this version yet.
