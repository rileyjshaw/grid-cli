# Public API

_Defined on Element 16 (System): Setup_

## Functions

```lua
iso_go(x, y) -- All ready
```

`x` and `y` are the current increments. That way, two modules plugged together with different increments don't interfere with one-another.

Would be much better if everything starts with a shared `GRID_X` and `GRID_Y`.

```lua
iso_gi(x, y) -- Grid increment
```

One of my favourite ideas in this whole codebase. (EDIT: Sad, it doesn't work!) At the start, every module calls `iso_gi(1, 0)` and `iso_gi(0, 1)`. This sends a message to the module to the right and the one above. On recieving a message, a module increments their axis value, then calls `iso_gi` on the module 1 further along the axis. This way, each module ends up knowing its coordinates within the grid.

This WAS a cool idea, but it doesn't work for certain L shapes. Here's the old function for reference:

```lua
function iso_gi(x, y)
  iso_gx = iso_gx + x
  iso_gy = iso_gy + y
  local c = string.format("if iso_gi then iso_gi(%d,%d)end", x, y)
  immediate_send(x, y, c)
end
```

```lua
iso_ir() -- Initialize rotation
```

Initializes the rotation of the module, so buttons can use their real world index.

```lua
iso_si(x, y) -- Set intervals
```

Updates `ISO_X` and `ISO_Y` to `x` and `y`. Called from a VSN1 module.

## Variables

```lua
iso_gx -- Grid X
iso_gy -- Grid Y
iso_ss -- Setup step
iso_r -- Rotation
iso_ri -- Real index

ISO_X -- X interval
ISO_Y -- Y interval
```
