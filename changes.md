# Changes

## Pause Bug Fix (2026-07-13)

### Problem
The game had a critical pause bug where the game loop continued accumulating time in the `accumulator` while paused. When unpausing, all the accumulated time would be processed instantly, causing a "time jump" that made the game fast-forward through all the missed frames.

### Root Cause
- The `gameLoop()` function always added `timestamp - lastTime` to `accumulator`, even when `state === 'paused'`
- The `update()` function only ran when `state === 'playing'`, so the accumulator kept growing
- On resume, the `while (accumulator >= TIMESTEP)` loop would process all accumulated frames at once
- Additionally, background animations (waves, clouds, islands, propellers) used `Date.now()` directly, so they continued animating while paused

### Solution
1. **Added pause tracking**: Introduced `pauseTime` variable to track when pause was initiated
2. **Fixed game loop timing**: On pause resume, reset `lastTime` to current time and `accumulator` to 0 to prevent time jumps
3. **Fixed animation timing**: Modified `draw()` function to use paused time when state is paused, stopping all visual animations
4. **Added state checks**: Modified background drawing functions (`drawOcean`, `drawClouds`, `drawIslands`) to skip position updates when paused
5. **Updated drawing functions**: Modified drawing functions to accept time parameter instead of calling `Date.now()` directly:
   - `drawPlayerPlane()` - now takes `t` parameter for invincibility flashing and propeller animation
   - `drawZero()` - now takes `t` parameter for propeller animation
   - `drawPowerUpItem()` - now takes `t` parameter for bobbing and glow animation

### Files Modified
- `index.html`: 
  - Added `pauseTime` variable (line 838)
  - Modified pause/resume key handler to reset timing (lines 1096-1108)
  - Modified `draw()` to use paused time (line 1026)
  - Modified `drawOcean()`, `drawClouds()`, `drawIslands()` to skip updates when paused
  - Updated drawing functions to use time parameter

### Testing
- Game now properly pauses all gameplay and visual animations when P is pressed
- No time jump occurs when resuming from pause
- Background elements (waves, clouds, islands) freeze in place during pause
- Player and enemy propellers stop spinning during pause
- Power-up bobbing and glow effects freeze during pause

### Impact
- Critical bug fix that makes the pause function work as intended
- Improves gameplay experience by allowing proper pauses without time jumps
- No performance impact - minimal overhead from state checks