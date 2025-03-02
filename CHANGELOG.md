# Change log

Popmotion adheres to [Semantic Versioning](http://semver.org/).

## [5.0.0] 2016-03-29

### Popmotion 5.0: timelines, streamlined API, tween blending, still 12kb.

**Warning:** This is a major API revision. Previous Popmotion code **will** be incompatible with this upgrade.

### Added
- **Timelines**: Super-simple yet fully-featured nestable timelines to easily sequence `tweens`.
- **Tween blending**: Smooth transitions between overlapping tweens.
- **Standalone actions**: `tween`, `physics` and `track` can all run without the need for an `actor`.
- **Adapters**: Minimal `get`/`set` API wrappers for smoothing differences between DOM, SVG and frameworks.
- **Transformers**: Composable functions to transform values between update and render.
- **Unified physics engine**: Handles `velocity`, `friction` and `spring` in one unified `physics` action.
- **Small**: All this for less than 12kb minified & gzipped.
- **Smaller**: Rewritten entirely using ES6 exports to allow tree-shaking, ignoring the parts of Popmotion you don't include.
- **Global time dilation**: `setGlobalDilation` method can change the global time.
- **Flow layer**: Replaces Actors and can work entirely in the background to manage multiple actions on the same object.
- Support `points` property for `polygon` and `polyline` tags.
- **MIT**: Changed licence to MIT.

### Removed
- `new` - dropped in favour of factory functions (ie `new Tween()` becomes `tween()`). This will allow further non-API-breaking optimisations.
- `Actor` dropped in favour of `flow`. The Actor model was monolithic, flows are automatically generated for `element`s in the background and can be accessed optionally via `detectFlow`.
- `process`: Now `task`. Prevents conflict with global common in browsers.
- Removed Action `watch` property in favour of more flexible `transform`: Simply provide a function that returns a different value.
- Native Meteor support, as we kept forgetting to update it.
- jQuery support - provide elements as returned from `$('.yourElement').get()` instead.
- `Sequence`: Dropped in favour of the `timeline` function.
- `Iterator`: Dropped in favour of using native array methods and the new `stagger` function.
- `Simulate`: Dropped in favour of unified `physics` action.

### Changed
- `friction` now a value between `0` and `1` - `0` provides no friction, `1` will strip all velocity within a single frame.

## [4.3.4] 2015-12-30

### Fixed
- `Simulate.hasChanged` incorrectly calculated. 

## [4.3.3] 2015-12-29

### Fixed
- Added `acceleration` to list of properties that can be set as functions, resolved when an Action starts.

## [4.3.2] 2015-12-26

### Fixed
- Recursion bug with `Actor.sync` under specific circumstances.

## [4.3.1] 2015-12-24

### Removed
- `deceleration` from `Simulate`.

### Fixed
- Fixed bug where `Tween` would start as ended if initalised during `update` ie via a `Sequence`.

## [4.3.0] 2015-12-17

### Added
- `scale` value type hooked up to CSS and SVG roles.
- `utils.camelToDash` utility function for converting camelCase props to dash-case.

### Changed
- Default `Simulate` `stopSpeed` changed from `5` to `0.0001` to account for tiny numbers like 0-1.

## [4.2.7] 2015-12-09

### Fixed
- SVG properies set ie `fillOpacity` are now getting set as `fill-opacity`.

## [4.2.6] 2015-12-08

### Fixed
- Fixed recursive loop when splitting Actor values.

## [4.2.5] 2015-12-07

### Added
- `opacity`, `fillOpacity` and `strokeOpacity` to `ui.svg` Role type map.

## [4.2.4] 2015-12-07

### Added
- `Simulate.autoEnd` property, set to `false` to prevent simulations from automatically ending.

### Fixed
- TweenControls `reverse` now work on completed Tweens.

## [4.2.3] 2015-12-06

### Added
- Actors automatically `sync` on init.

## [4.2.2] 2015-12-03

### Update
- Moving from Babel's official es2015 preset to a custom build.

## [4.2.1] 2015-12-03

### Update
- Updating Babel to fix transpilation errors in IE10.

## [4.2.0] 2015-12-02

### Changed
- Moving to dual commericial and GPLv3 licence.

## [4.1.0] 2015-11-28

### Added
- Actor value `watch` property can now be a function returning any numerical value.
- Added `smooth` for all actions.
- Added `calc.toDecimal` calculator function. 

## [4.0.0] 2015-11-20

### Added
- New core processing loop. Seperates processes into four stages: `update`, `preRender`, `render`, `postRender`.
- `Process.once` to fire a Process for a single frame.
- Run background processes by passing `true` to `Process.setBackground` or as the last argument to the `Process` constructor. Background processes won't spin up the process loop when activated, only running when non-background processes are active.

### Changed
- `new ui.Process()` takes `callback, scope` instead of `scope, callback`.
- `Process` callbacks now receive `scope` as the first argument, then `framestamp, frameDuration`.

### Removed
- `Process.every`, `Process.reset` and `Process.fire`. Processes should only be started/stopped with `Process.start` and `Process.stop` respectively, to ensure they're run as part of the main loop. `every` is redundant with a combination of `setInterval` and `Process.once`.
- `Process.start` no longer takes a time period as an argument - use `setTimeout` to `Process.stop`.

## [3.8.1] 2015-11-19

### Fixed
- Pow easings incorrectly named var.

## [3.8.0] 2015-11-19

### Added
- Elliot Geno's awesome `'anticipate'` easing. Follow him at [@ElliotGeno](https://twitter.com/ElliotGeno/).
- In-built easings now available in the `ui.ease` namespace. So instead of providing `'backOut'` you can reference it literally - `ui.ease.anticipate`. 
- Create modified easing function strengths, for instance `ease: ui.modifyEase(ui.ease.backOut, 2)`. `'ease'` and `'back'` in/out/inOut variants and `'anticipate'` are available. You must provide the literal reference rather than string reference.

## [3.7.1] 2015-11-11

### Changed
- Refactored core clock to increase performance in lower-end devices.

## [3.7.0] 2015-11-07

### Changed
- Software licence changed. Popmotion is now free for non-commercial uses, and requires a per-project licence for commercial projects.
- More files converted to ES6 syntax.
- Moved back to small for production compilation.
- Upgraded Babel from 5 to 6.

### Added
- Beginning suite of Mocha unit tests.

## [3.6.3] 2015-11-03

### Added
- Extra tests to ensure Popmotion is loading correctly in Meteor.

### Fixed
- Explict test for rAF for when `window` is available and `requestAnimationFrame` isn't. 

## [3.6.2] 2015-11-02

### Added
- Meteor support. Published on [Atmosphere](https://atmospherejs.com/popmotion/popmotion) as `popmotion:popmotion`.

### Fixed
- `performance` and `window` checks in Node.

## [3.6.1] 2015-10-29

### Fixed
- Smoothing lower than frameduration produced odd values.
- Smooth by `0` `Infinity` error

## [3.6.0] 2015-10-29

### Added
- New `transform(value, key, actor)` property for `Actor` values. Allows you to return a new value after its been processed by an action, but before it's been limited/rounded etc.
- Exposed our `Track` `smooth` calculator as `ui.calc.smooth`.

### Changed
- Refactored some files to cut down on filesize.

### Fixed
- Fixed a regression from `3.3.3` that fixed `performance` in IE9.

## [3.5.0] 2015-10-21

### Added
- Roles are now getter/setters, if `get` and `set` methods are present. For example: CSS role has getter/setters, so you can call:

    ui.css(element, {
        position: 'absolute',
        top: 0
    });

## [3.4.4] 2015-10-22

### Fixed
- `Actor.stop().start()` was failing to run.

## [3.4.3] 2015-10-21

### Fixed
- `Actor.sync` now returns `Actor` rather than the bound sync `Action`.

## [3.4.2] 2015-10-21

### Fixed
- `svg` tags are now assigned `ui.css` role.

## [3.4.1] 2015-10-17

### Fixed
- Delaying test element creation in CSS Role prevents error in server-side rendering.

## [3.4.0] 2015-10-16

### Added
- `Sequence` class, for creating a sequence of non-sequential actions.
- `onComplete` property to `Iterator.stagger`.
- Pass an action as the `Iterator.each` and `Iterator.stagger` `method` argument to automatically run `start` on each `Actor`.

### Changed
- Using rAF-provided timestamp instead of `performance.now` for smoother motion.

## [3.3.3] 2015-10-13

### Fixed
- @stoikerty: Fixed `performance.now` check for IE9.

## [3.3.2] 2015-10-10

### Fixed
- `Pointer` events now properly unbound on `Actor` stop.

## [3.3.1] 2015-10-09

### Added
- `Actor.smooth` now settable on a per-value basis.
- `direct` value property added to take direct input values instead of inputOffset.

## [3.3.0] 2015-10-08

### Added
- `smooth` property added to `Track` - smoothes out values coming from `Input` sources.

## [3.2.1] 2015-10-07

### Fixed
- `watch` no longer overwritten on `set`.

## [3.2.0] 2015-10-06

### Added
- `ui.select` now caches and finds cached Actors bound to DOM elements. If one Actor is found, it returns an Actor. If multiple Actors are found, an Iterator.
- `reverse` method to `Iterator`.

## [3.1.7] 2015-10-05

## Fixed
- Adjusting `hasChanged` logic to always fire on first frame.
- Changing `Iterator.stagger` logic for more even staggers. 

## [3.1.6] 2015-10-05

## Fixed
- Manually moved the library class filenames to uppercase.

## [3.1.5] 2015-10-05

## Fixed
- Renamed some class files to uppercase to fix include fails in some Browserify compilations.

## [3.1.4] 2015-10-05

## Added
- Simulation functions are now sent `value <object>, frameDuration <int>, timeStarted <timestamp>` as arguments.

## [3.1.3] 2015-10-04

## Fixed
- Actions fired within an `onComplete` wouldn't start because the number of active Actions was being counted incorrectly.

## [3.1.2] 2015-10-03

### Fixed
- Major Firefox bug 1) `values` false-positive test for `watch` property, now explicitly checking for `string`.
- Major Firefox bug 2) `element.style.hasOwnProperty()` always returning false, switching to `in element.style`.

## [3.1.1] 2015-10-02

### Fixed
- Clearing Actor then/next queue on `start`.
- Saving all arguments to queue via `then` so we can pass Inputs.

## [3.1.0] 2015-10-01

### Added
- Action-specific `onStart`, `onUpdate`, `onFrame` and `onComplete` callbacks. These callbacks will be active only for the duration of the action, while callbacks attached to the host Actor will persist through all actions.

### Changed
- `onStart` callbacks are now fired immediately before the Actor is activated, giving actions extra time to initiate and make use of the [< 100ms response window](https://aerotwist.com/blog/flip-your-animations/).

### Fixed
- Bugfix for deep-copying Actions on Action start. That was a whoops and a half.

## [3.0.4] 2015-09-30

### Fixed
- Bugfix for subvalues not being flipped correctly.

## [3.0.3] 2015-09-30

### Fixed
- SVG Role divide by 0 error when `scale` === 0.

## [3.0.2] 2015-09-29

### Fixed
- Bugfix where Popmotion would attempt to split numerical values.
- Bugfix for `complex` valueType regex where negative numbers were made positive.

## [3.0.0] 2015-09-29

### Added
- Full SVG support.
- Multiple simultaneous Actions on a single Actor - mix Simulations, Tracking and Tweens on the same elements!
- Animate complex strings, like `path` `d` attributes.
- Iterator - to allow single classes to be extended the ActorCollector has been dropped in favour of a generic Iterator class, which can iterate over any set of classes. This also makes it clearer when you're interacting with multiple items vs a single Actor, and these items are not longer limited to Actors.
- Roles - `ui.css`, `ui.attr`, `ui.svg`, `ui.draw`. These are auto-assigned to Actors when initialised with an `element` property, but can also be manually assigned with the `as` property on Actor initialisation.
- Actors can have multiple roles by providing an array to `as`.
- New roles can be created with `new ui.Role()`.
- Value names can be translated before a Role accesses it, via a Role's `map` property. For example `ui.cssRole` maps `x` to `translateX`.
- Action classes/definitions - `Tween`, `Simulate`, `Track`

### Removed
- `ui.addRoute` - see Roles
- `ui.addPreset`, `ui.addAction` - see Tween, Simulate and Track classes
- `ActorCollection` - see Iterator
- `play`, `run`, `track` Actor methods - use `start`

### Changed
- `addToQueue` Actor method is now `then` and takes Tween, Simulate and Track instances instead of raw properties.
- `mapLink` Actor value property is now `mapFrom`.
- Default tween `duration` set to `300`.
- Default tween `ease` set to `"easeOut"`.
- `reverse`, `reset` -> `restart`, `seek` methods moved to `TweenControls` (returned when a `Tween` is passed to `start`)

### Deprecated
- `flipValues`, `reverse`, `reset`, `resetProgress`, `resetOrigins` and `seek` Actor methods - these are all going to be moved to the `Tween` class in `3.2.0`

## [2.0.4] 2015-08-10

### Fixed
- Fixing `bounce` and `capture` simulation calls.

## [2.0.3] 2015-08-10

### Removed
- Removed undocumented `ui.addSimulation` - new simulations now passed as function instead of simulation name.

## [2.0.2] 2015-08-10

### Changed
- `Actor.seek` no longer an Action, much higher performance.

## [2.0.1] 2015-08-07

### Changed
- Only numerical properties can be set as functions to be resolved on action start.

## [2.0.0] 2015-08-07

### Removed
- `ui.addEasing()`

### Added
- New easing functions are now generated with `new ui.Easing()` and provided as the `ease` property. When provided an easeIn function, `in`, `out` and `inOut` methods are returned.

## [1.0.0] 2015-08-06

**Note:** Forked from Redshift v2.1.1.

### Changed
- `redshift` object name now `ui`.
- Terminology changes to fix API semantics:
    - **Action:** Actor
    - **ActionCollection:** ActionCollection
    - **Rubix:** Action (as in, an Action an Actor can perform)

### Added
- Add new easing functions with `ui.addEasing()`. Provide the easeIn function and Popmotion will generate easeOut and easeInOut variants.
- Add new simulation functions to `run` with `ui.addSimulation()`.
- Any value can be a special **value type**, ie a color. `'#FFF'` splits into four numerical properties, `Red`, `Blue`, `Green` and `Alpha`.
- Add new value types with `ui.addValueType()`.
- HSLA value type support.

## [2.1.1] 2015-06-11

### Fixed
- Change Action `rubix` from `"seek"` to `"play"` onEnd.

## [2.1.0] 2015-06-11

### Added
- Added `.seek()` method to Actions.

## [2.0.5] 2015-06-02

### Added
- ActionGroup returns array of values when a getter is called.

## [2.0.4] 2015-06-01

### Fixed
- `onStart` regression from 2.0.0 - only firing for 'values' route.

## [2.0.3] 2015-06-01

### Fixed
- Fixing hasChanged regression, prevented .run() from stopping automatically.

## [2.0.2] 2015-06-01

### Fixed
- Adding Alpha property to all split color values (default: 1), in case a value has mixed RGB and RGBA properties.

## [2.0.1] 2015-06-01

### Added
- CSS values travelling through a splitter (ie backgroundColor is split into RGB values) can be set as functions like normal values.

## [2.0.0] 2015-06-01

### Changed
- Upgraded stepped easing algorithm.
- `Action.hasChanged` set to `true` when `Action.isActive(true)`

### Removed
- `.props()` method removed - properties now saved directly to Action object.
- `.data()` functionality removed, just set properties of Action instead.
- `.flip()` is now `.flipValues()`.

## [1.4.1] 2015-05-31

### Fixed
- ActionGroup.stagger() wasn't returning `this`

## [1.4.0] 2015-05-31

### Added
- Action Groups for controlling multiple Actions at once.
- Stagger method for Action Groups.
- DOM selection support for creating Actions prepopulated with DOM elements.

### Fixed
- Calling .play(preset) while Action was in progress failed to add that call to the play queue.
- Added check for Process timers before clearing as clearTimeout is costing ~.4ms.
