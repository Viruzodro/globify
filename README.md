# Globify

Hello. I've been building my own world for the majority of my life, and there are some tools I've been wanting to make for a while, which i now have made. Having a good way to track distance has plagued me, I also always have a hard time picturing distance on a flat map. So I made Globify.

You drop in your map image and it wraps onto a 3D globe you can spin around. Then you drop pins along a route and it gives you real distances, plus how long it takes to travel them on foot, by wagon, on horseback, at forced march, or under sail.

**[Open it](https://viruzodro.github.io/globify/)**  ·  **[Download](https://github.com/Viruzodro/globify/releases/latest)**  ·  **[Buy me a coffee](https://ko-fi.com/viruzodro)**

![A world map turning as a globe](demo.gif)

It's free and runs in your browser. Your map never leaves your computer, since there's no server involved at all. It's one HTML file with everything baked into it, so you can download it and use it offline forever. No need to install anything.

## Your map

Use a 2:1 image, twice as wide as it is tall, and leave it on Equirectangular. Anything else, switch to Mercator and hit *Use the undistorted span*.

Equirectangular takes the width of your image and wraps it around 360° of longitude, and takes the height and runs it across 180° of latitude. 360 divided by 180 is 2, which is where the 2:1 comes from. Every row of your image gets stretched to wrap a full circle around the globe. Near the equator that circle is huge. Near the pole it's almost nothing. So the top and bottom rows of your image get crushed down to a point.

Which means a real equirectangular map has to be drawn pre-stretched at the poles, so the crushing cancels out. That's why Antarctica is a giant white bar across the bottom of every world map you've ever looked at, in case you were curious.

so if your map looks correct sitting flat, it's probably closer to Mercator. Mercator squeezes latitude toward the poles by the exact amount the wrap is going to stretch it back out, so your shapes come out right. The tradeoff is it can't reach the poles at all. A 16:9 map covers about ±70° of latitude and the caps above and below get filled in with a color sampled from the edges of your image.

Two other things. Try to make the left and right edges of your map match, since they meet at the seam. And if you can't, the prime meridian slider moves the seam somewhere else so you can park it over an ocean.

There's also a template you can download. It comes out sized for whatever projection you're on and it's covered in circles. Every circle on that sheet turns into a true circle on the globe. So round marks mean your shapes survive, stretched ovals mean they don't.

## World shapes

This has been the most requested feature.

**Globe** wraps your map onto a sphere.

**Disc** reprojects it onto a flat circle, north pole in the middle, south pole spread all the way around the rim. That's the projection flat earth maps use, and it's why the ice wall goes where it does.

**Plate** just lays the map down flat at its own proportions.

Both flat shapes have an **Underside**, which is a craggy mass of rock hanging below the world, and an **Ice wall** around the edge. Either one can be toggled off.

## Measuring a journey

Turn on **Drop pins** and tap the globe. Dragging still spins it, only a tap that stays put drops a pin.

Pins connect with great circle arcs, which is the actual shortest path across a sphere. It's not the straight line your flat map shows you. Routes that cross high latitudes come out way shorter than you'd think.

Hit **Sea leg** to switch mid-journey, so a march to the coast followed by a crossing gives you better data. Land pins and legs are red, sea ones are blue, and one route can have as many of each as you want.

Tap a pin, or its row in the list, to select it. Then you can **Insert after** to stick a stop in the middle of a route you already built, or **Delete pin** to pull one out and let the route close up around it. Undo takes off the last one. Clear all wipes it.

You get distance per leg and total, in kilometers and miles at the same time, and land and sea get their own subtotals when you've used both. Travel time comes back for all five paces at once so you can compare them without changing a setting.

| Pace | Rate |
|---|---|
| On foot | 30 km/day |
| Wagon or cart | 25 km/day |
| On horseback | 50 km/day |
| Forced march | 60 km/day |
| Sailing ship | 190 km/day |

Those are sustained rates over mixed terrain, not a courier sprinting down a road. If your route has sea legs in it, the land paces already include the sailing time, and the sea portion gets listed separately underneath.

**Planet radius** is set to Earth at 6371 km. Change it if your world isn't Earth-sized and every distance rescales. Mars is 3390 for reference.

Two limitations you should know about. Sea legs take the same great circle as land legs, straight over whatever is in the way, so treat those numbers as a floor and not a real sailing route. Drop a few extra pins along the coast if you want something closer. And pins stick to the sphere, not to your image, so if you change projection after you've measured, the map slides around underneath them. Pick your projection first.

## Rings

Turn on **Rings** and a whole section shows up for them. **Inner** is where the ring starts, **Width** is how far out it goes, then **Opacity** and ten tints running white through brown plus a few greys.

There's also **Tilt**, which is separate from the planet's axial tilt. So you can stand the ring straight up if you want, and it holds that angle while the world keeps spinning.

The bands are generated instead of drawn, three layers of striations plus a few gaps including a big Cassini style division. The planet doesn't cast a shadow on the rings. That needs a custom shader and I haven't done it.

## Everything else

Axial tilt goes both directions now, -45° through 0 to +45°, and it sets the ring plane too. There's spin speed, a latitude and longitude grid, day/night lighting, a starfield, and an atmosphere halo. All toggleable.

If your map looks soft when you zoom in, that's the **2K / 4K / 8K** setting. Your image gets redrawn onto an internal sheet before it ever reaches the GPU, and that sheet's size is what limits detail, not your source file. It starts at 4K. only go to 8K if your source is actually that big, since it costs real memory for nothing otherwise.

## Exporting

**Save this view as PNG** grabs a still.

**Export a full turn as GIF** gives you a looping 360° spin, which is nice for a campaign doc or a Discord banner. You pick size, frame count, and how many seconds a turn takes. **Transparent** drops the background so it can sit on any page, though it turns off the starfield and halo, since GIF transparency is all or nothing per pixel and soft glows come out ragged. **Dither** cleans up banding in the shading and roughly doubles the file size.

Whatever you export shows up in a panel. Save it from the button, or press and hold the image if your browser blocks the download.

## Controls

| | Mouse | Touch |
|---|---|---|
| Spin | Drag | Drag |
| Move | Shift-drag or right-drag | Two-finger drag |
| Zoom | Scroll | Pinch |
| Re-center | Double-click | Center button |

## Couple of three things

HEIC images won't load. No browser can decode them, so export as a JPG first. You can also paste an image straight out of your clipboard if that's easier.

If a save button does nothing, your browser is blocking it. Press and hold the preview image instead, or download the file and open it directly instead of through a preview pane.

## Built with

[Three.js](https://threejs.org) r128, embedded in the file. Fonts are Spectral and IBM Plex Mono, also embedded. The GIF encoder is written from scratch.

anyway. I built this for my own campaign, so if something is missing, let me know. I'm hyperfixated on this right now so, I'll likely be able to add it fairly quickly, or at least until the ADHD juice runs out.

## License

MIT, see [LICENSE](LICENSE).
