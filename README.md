# Globify

Wrap a flat map onto a 3D globe in your browser, then export a looping GIF of it turning.

Built for worldbuilders who have a map and want to see what their world actually looks like as a planet.

**[Try it in your browser](https://viruzodro.github.io/globify/)**  ·  **[Download it to keep](https://github.com/Viruzodro/globify/releases/latest)**  ·  **[Buy me a coffee](https://ko-fi.com/viruzodro)**

![A world map turning as a globe](demo.gif)

## What it does

- Drop in a JPG or PNG and see it wrapped on a sphere immediately
- Reads your map as either **equirectangular** or **Mercator**, which is what determines whether your continents keep their shapes
- Adjustable latitude span, so your art can stop short of the poles instead of pinching to a point
- Movable prime meridian for hiding the seam behind an ocean
- **Journey measuring**: drop pins on the globe and get true great-circle distances in both kilometres and miles, per leg and total, with travel time on foot, by wagon, on horseback, at forced march, and under sail
- Set your planet's radius, so distances are right for your world and not just Earth's
- Axial tilt, spin rate, graticule overlay, sunlight shading, starfield, atmosphere halo, and a banded Saturn-style ring system
- Downloadable drawing templates with distortion marks, sized for whatever projection you pick
- Exports a still PNG or a seamless looping GIF of a full 360° turn

## Nothing is uploaded

Your map never leaves your computer. There is no server, no account, no analytics. The page reads the file locally and does all rendering and encoding in your browser.

## Works offline

`index.html` is completely self-contained. Three.js and both typefaces are embedded in the file. Download it, open it, and it works with your wifi off, forever.

## What aspect ratio should my map be?

For **equirectangular**, exactly 2:1. Width must be double the height, because the projection spreads the full width across 360° of longitude and the full height across 180° of latitude. Good sizes are 2048×1024 or 4096×2048.

For **Mercator**, any aspect ratio works. A 16:9 map covers about ±70.6° of latitude, and the poles above and below get filled with a cap color sampled from your map's edges.

If your flat map looks correct to your eye, it is probably closer to Mercator than equirectangular. A true equirectangular map has to be drawn pre-stretched, with the polar regions smeared absurdly wide, so that the stretching cancels out once it wraps. That is why Antarctica looks enormous on a world map.

Use the **Download template** button to get a guide sheet at the right dimensions. Every circle on it becomes a true circle on the globe, so round marks mean your shapes will survive.

One more thing: make the left and right edges of your map match, since they meet at the seam.

## Measuring a journey

Turn on **Drop pins**, then tap the globe to place them. Dragging still spins the globe; only a tap that stays put drops a pin. Each pin connects to the last one with a great-circle arc, which is the genuinely shortest surface route between two points on a sphere and not the straight line your flat map suggests.

Toggle **Sea leg** at any point to switch the journey between overland and sailing. Land legs and their pins are red, sea legs are blue, and a single journey can mix them freely. Distances are totalled separately, and the sailing pace only appears once there's water to cross.

Distances show in kilometres and miles at once, per leg and as a running total. Underneath, travel time is listed for five paces simultaneously, so you can compare a march on foot against a ride or a sea crossing without changing any setting.

Distances assume Earth's radius of 6371 km by default. Change **Planet radius** to match your world. A few reference points: Mars is 3390, a small habitable world might be 4000, and doubling the radius doubles every distance.

The daily rates are sustained historical figures, not best-case sprints. On foot at 30 km/day is a reasonable pace for a party carrying gear over mixed terrain.

## Controls

| Action | Mouse | Touch |
|---|---|---|
| Spin the globe | Drag | Drag |
| Move the globe | Shift-drag or right-drag | Two-finger drag |
| Zoom | Scroll | Pinch |
| Re-center | Double-click | The Center button |

## GIF export notes

- **Transparent** removes the background so the globe can sit on any page. It turns off the starfield and halo, because GIF transparency is strictly on or off per pixel and soft glows come out with ragged edges.
- **Dither** hides color banding in the shading. GIF holds only 256 colors, so smooth gradients would otherwise break into stripes. Costs roughly double the file size.
- A single palette is built across the whole rotation rather than per frame, which is what keeps the loop from shimmering.

If the save button does nothing, press and hold the preview image and choose Save image. Some browsers block downloads from embedded frames.

## Running it yourself

Download `globify.html` from the [latest release](https://github.com/Viruzodro/globify/releases/latest) and double-click it. That's the whole install. No dependencies, no build step, no internet needed after the download.

## Built with

[Three.js](https://threejs.org) (MIT). Typefaces are [Spectral](https://fonts.google.com/specimen/Spectral) and [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono), both SIL Open Font License 1.1. The GIF encoder is written from scratch in this file: median-cut quantization, Floyd-Steinberg dithering, and LZW compression, with no dependencies.

## Support

Globify is free and always will be. If it saved you time or you just like it, you can [buy me a coffee on Ko-fi](https://ko-fi.com/viruzodro). Entirely optional, and it doesn't unlock anything.

## License

MIT. See [LICENSE](LICENSE).
