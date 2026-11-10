# React Sample App Debugging Report

## Purpose and environment

This report records the debugging process, the issues found, the fixes implemented, and verification performed for the React Bug Shop sample app.

The app was run locally with `npm start` and inspected in the integrated browser. React Developer Tools was not available in that browser session, so the component tree was not inspected through the extension. Instead, the running UI, component source, and built-in **collect observations** checks were used. The steps below describe what was actually performed.

## Debugging process

1. Reviewed the app entry points, challenge routes, component props/state, and each scenario's `useBugTest` assertions.
2. Started the development server and visited the affected bug routes in the browser.
3. Compared the visible component output with its observation checks. Reproduced behavior using the page controls: change spider/caterpillar levels, choose moth props, toggle pillbug and centipede ratings, change quantities, select a store, type `mosquito`, open Reviews, and disable Strict Mode.
4. Traced each failing observation to the relevant state initialization/update, prop contract, effect dependency, or synchronous render work.
5. Applied targeted fixes and repeated the interactions. Confirmed the corresponding observation panels turned green and the app production build succeeded.

## Issues and solutions

| Component/scenario | Issue identified | Solution |
|---|---|---|
| Shy Spider — [UnexpectedState.js](./src/bugs/UnexpectedState.js) | Initial level prop was missing, `useState` tuple was treated as the value, and level changes did not use a state setter. | Passed the initial level; updated state and purchase summary when the level changes. |
| Umbrella Moth — [UnexpectedPropTypes.js](./src/bugs/UnexpectedPropTypes.js) | Popularity used the wrong value type, rating `0` was hidden by a truthiness check, and `null` inventory was treated like low stock. | Passed expected values, rendered non-null ratings, and handled unknown inventory as in stock. |
| Crimson Caterpillar — [ChangingProps.js](./src/bugs/ChangingProps.js) | Like changes only modified a local variable, while level-up logic mutated the received attributes object. | Moved Like to React state and derived adjusted attributes immutably. |
| Pilfering Pillbug — [PassingProps.js](./src/bugs/PassingProps.js) | Initial purchase level and summary prop names did not match their consumers; checks needed to remember the initial anonymous-like state. | Passed matching props, initialized level, made the rating controls usable, and retained the appropriate successful observation. |
| Confounding Cricket — [product-service/index.js](./src/product-service/index.js) | The discount check created a checksum array whose size grew exponentially with quantity. | Replaced the unnecessary checksum pipeline with a finite-quantity and threshold check. |
| Dapper Dragonfly — [DelayedRender.js](./src/bugs/DelayedRender.js) | Currency parsing included an artificial busy loop that blocked updates. | Removed the loop; retained the currency calculation. |
| Defiant Damselfly — [DeferredRender.js](./src/bugs/DeferredRender.js) | Filtering was deferred, but every suggestion label still performed a blocking busy wait. | Removed the artificial blocking render; deferred filtering remains. |
| Emerald Ash Borer — [ExcessiveRender.js](./src/bugs/ExcessiveRender.js) | The quantity picker disappeared while refetching, and an unstable callback could trigger repeated query work. | Kept the picker mounted and stabilized its callback. |
| Huggable Honeybee — [HookSideEffects.js](./src/bugs/HookSideEffects.js) | Unstable refetch callbacks, mutable analytics batches, and an uncleared timer caused excess effects or incorrect cleanup. | Stabilized callbacks, updated batches immutably, avoided posting to an unavailable static-file endpoint, and cleared the interval on unmount. |
| Cheerful Cicada — [ContextRender.js](./src/bugs/ContextRender.js) | Store-card items re-rendered unnecessarily when selecting a home store. | Memoized store items and passed stable per-card selection values. |
| Curious Centipede — [CascadingRender.js](./src/bugs/CascadingRender.js) | The heart badge remounted and regenerated its animation on unrelated parent renders. | Memoized the badge component. |
| Lovable Ladybug — [LongRunningRender.js](./src/bugs/LongRunningRender.js) | Rendering the large review list blocked urgent tab interaction. | Scheduled the tab change as a transition and made its intermediate observation persistent. |
| Silent Stag Beetle — [StrictMode.js](./src/bugs/StrictMode.js) | Development Strict Mode intentionally replays mounts, so the initial counter shows two. | Kept the demonstration behavior; verified that **Disable Strict Mode** changes the count to one. |

## Verification

- The umbrella moth checks passed for trending status, 3.5 rating, and in-stock status.
- The spider state/summary checks passed. The caterpillar Like and level-up/reset checks passed.
- The pillbug checks passed after selecting Like and then Dislike; summary and heading checks passed.
- The context-render check passed after choosing a home store. The honeybee quantity/refetch/analytics/timer checks passed after quantity changes.
- The cricket reached quantity 50 with its discount check passing; the dragonfly reached quantity 10 with its update check passing.
- Typing `mosquito` passed the damselfly delay check. Opening Reviews passed the ladybug observation. Disabling Strict Mode passed the stag beetle mount check.
- `npm run build` completed successfully.
- `npm test -- --watchAll=false` reported no test files found. These challenge checks are rendered in the app rather than maintained as Jest test files.

## React Developer Tools steps for a local browser

The integrated browser used for this run did not expose the React Developer Tools extension. To repeat the inspection with the extension in a regular browser:

1. Install React Developer Tools using the [official React Developer Tools guide](https://react.dev/learn/react-developer-tools).
2. Run `npm start` and open `http://localhost:3000`.
3. Open browser Developer Tools and select **Components**.
4. Select a bug component to inspect its props, state, and hooks. Reproduce the behavior using its controls and compare the component data with the app's observation checks.
5. For performance scenarios, open **Profiler**, record an interaction (such as choosing a store or opening Reviews), and inspect which components rendered and how long they took.

