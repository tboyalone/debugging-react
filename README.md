# Getting Started with the React Bug Shop Demo

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/kamranayub/pluralsight-course-react-debugging)

The fastest way to jump into the demo experience and solve the challenges is by running in the GitHub Codespace which is a preconfigured development environment with everything you need to follow along with the course.

Once you're in, simply run:

    npm start

To start the dev server, and Codespaces will prompt you to open a hosted URL in the browser to view the app.

Alternatively, you can clone the project locally and configure your own local dev environment.

## Solving the Challenges

The goal is to catch all the bugs in the shop. Each bug comes with a set of checks you need to make pass. You'll need to refactor and update the code.

The videos in the course provide the solutions to each challenge but there are often multiple ways to solve a problem with React. If you're stuck, reference the videos or explore on your own!

## Debugging with React Developer Tools

1. Start the app with `npm start` and open `http://localhost:3000`.
2. Install the React Developer Tools browser extension from the [official React Developer Tools page](https://react.dev/learn/react-developer-tools), then open the browser's developer tools.
3. Use the **Components** panel to find the bug component. Inspect its props, state, and hooks; use **Profiler** to record renders while reproducing performance scenarios.
4. Compare the component state and props with the displayed output. The built-in **collect observations** panel also runs scenario checks. Complete the required interactions until all checks pass, then catch the bug.

### Debugging process and fixes

- Compared each challenge's rendered output with its component props and hooks, using the observation panel to isolate incorrect values and interactions.
- Initialized the spider's purchase level, used the state setter for level changes, and kept its purchase summary in sync.
- Used state for the caterpillar's like control and derived leveled attributes without mutating incoming props.
- Corrected the moth's popularity/rating values and handled a null inventory count.
- Fixed the pillbug's prop flow and summary inputs; retained successful intermediate observations while testing like/dislike and review-loading interactions.
- Replaced the volume-discount checksum's exponential allocation with its equivalent threshold check, and removed the dragonfly's blocking currency loop.
- Deferred address filtering and removed the blocking suggestion-label render, kept the quantity picker mounted during promotion refetches, stabilized callbacks, batched demo analytics events immutably without posting to a missing static-file endpoint, and cleaned up the sale timer.
- Memoized stable store cards and the centipede's animation badge, and used a transition so the ladybug's reviews do not block urgent UI updates.
- The stag beetle's Strict Mode behavior is intentional; use **Disable Strict Mode** to compare its mount count.

The challenge checks run in the app rather than as Jest test files. `npm test -- --watchAll=false` reports that no test files were found; use the browser checks above and `npm run build` to validate the app.

---

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
