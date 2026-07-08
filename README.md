# Saltmire FX

**One-line 2D sprite shader effects for Godot 4.** Dissolve, outline, hit-flash, freeze, and hologram — drop in the addon and call one line. No setup, no dependencies.

```gdscript
FX.hit_flash($Sprite2D)              # white damage flash
FX.dissolve($Sprite2D)               # burn away with a glowing edge
FX.appear($Sprite2D)                 # materialize in (reverse dissolve)
FX.outline($Sprite2D, Color.YELLOW, 2.0)
FX.freeze($Sprite2D)                 # icy tint
FX.hologram($Sprite2D)               # animated sci-fi look
FX.clear($Sprite2D)                  # remove the effect
```

## Effects

| Call | What it does |
|------|--------------|
| `dissolve(target, duration=0.5)` | Burns the sprite away with a glowing edge. Returns a `Tween`. |
| `appear(target, duration=0.5)` | Reverse dissolve — materialize in. Returns a `Tween`. |
| `hit_flash(target, color=WHITE, duration=0.15)` | Blend to a solid color then fade back. Returns a `Tween`. |
| `outline(target, color=WHITE, width=1.0)` | Persistent pixel-perfect border. |
| `freeze(target, to=1.0, duration=0.2)` | Desaturate + icy blue tint. Returns a `Tween`. |
| `hologram(target, amount=1.0)` | Animated scanlines, tint, and flicker (self-animating via `TIME`). |
| `clear(target)` | Removes any Saltmire FX material from the target. |

The methods that animate return the `Tween`, so you can `await` them:

```gdscript
await FX.dissolve($Enemy, 0.6).finished
$Enemy.queue_free()
```

## Install

1. Copy `addons/saltmire_fx/` into your project's `addons/` folder.
2. Enable **Saltmire FX** in *Project → Project Settings → Plugins*.
3. The `FX` singleton is now available everywhere. That's it.

## Notes

- Works on any `CanvasItem` (Sprite2D, AnimatedSprite2D, TextureRect, etc.).
- Effects are applied one at a time — each call assigns a `ShaderMaterial`, and the last one wins. Use `clear()` to restore the default material.
- Shaders use in-shader value noise, so there are **no texture dependencies** — just a handful of small `.gdshader` files.
- Aspect-independent; works at any resolution.

Part of the **Saltmire** game-feel family — pairs with:
- [Saltmire Juice](https://saltmire.itch.io/saltmire-juice) — screen shake, hit-stop, damage numbers.
- [Saltmire Transitions](https://saltmire.itch.io/saltmire-transitions-scene-transition-kit-for-godot-4) — one-line scene transitions.

## ⚡ Want the whole combo in one call?

[Juice](https://saltmire.itch.io/saltmire-juice), FX, [Trail](https://saltmire.itch.io/saltmire-trail), [Spark](https://saltmire.itch.io/saltmire-spark) and [Transitions](https://saltmire.itch.io/saltmire-transitions-scene-transition-kit-for-godot-4) are free and standalone. **[Saltmire Impact](https://saltmire.itch.io/saltmire-impact)** wires the whole family into one-line combo hits — shake + flash + particles + slow-mo from a single call. If FX saved you time, Impact saves you the wiring.

## License

MIT — read it, fork it, ship it. See [LICENSE.txt](LICENSE.txt).
