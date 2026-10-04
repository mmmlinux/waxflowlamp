# Wax Flow Lamp

A 3D wax lamp that runs in your browser. It's a single HTML file with no dependencies and no build step.

**Live:** https://mmmlinux.github.io/waxflowlamp/

## Using it

Open `index.html` in any modern browser, or visit the live page.

- **Drag** the lamp sideways to turn it. With a mouse, drag up or down to tilt it.
- **Double-click** to reset the tilt.
- **Scroll down** for the controls. The lamp shrinks to stay in view above the panel.

## Controls

All groups start collapsed so the lamp stays the focus.

| Group | What it does |
| --- | --- |
| Presets | Colour schemes for the wax, liquid and base, plus Random |
| Power & heat | Power on/off, heat, flow speed, viscosity |
| Wax | Colour, amount, blob size, gooeyness |
| Liquid & light | Liquid colour, haze, bulb brightness |
| Lamp | Base finish (chrome, brushed, gold, copper, black), glass refraction |
| View | Turntable, turn speed, zoom |
| Performance | Render quality, automatic quality drop when slow, frame rate |

Settings are saved in your browser. **Reset all** restores the defaults.

## How it works

- **Rendering:** a WebGL fragment shader raymarches the lamp. The glass, base and cap are signed-distance solids of revolution. Rays bend as they enter the glass and pick up tint and haze from the liquid. The light comes from the bulb below the wax.
- **Wax:** each blob is a stretched, slowly shifting lumpy ellipsoid. Blobs join the pool with a gooey neck, but blobs that touch each other meet at a tight seam unless they are fusing.
- **Physics:** each blob has a temperature. The pool heats it, the liquid cools it (most strongly near the top), and buoyancy follows temperature. A blob leaves the pool only once it's hot enough, and leaves the top only once it's cool enough. This hysteresis gives the slow, staggered cycle.
- **Contact and fusion:** blobs that meet press together and usually slide past. A fusion bond builds while they touch, faster when they press deeper and when their temperatures are close. Some pairs are sticky and fuse on impact. A fusing pair grows a neck, then the smaller blob drains into the larger. Big merged blobs sometimes pinch off a trailing piece, and merged wax breaks up again in the pool.
- **Performance:** the shader renders below screen resolution and lowers resolution further when frames get slow.

## Debug URL parameters

| Parameter | Effect |
| --- | --- |
| `?sim=30` | Run the simulation forward 30 extra seconds before the first frame |
| `?scale=0.5` | Fix the render resolution and turn off automatic quality |
| `?yaw=1.2` | Start the lamp turned by this many radians |
| `?panel` | Open the first two control groups and scroll to the controls |

## License

[MIT](LICENSE)
