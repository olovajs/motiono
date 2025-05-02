# `motiono`: A GSAP-Powered React Animation Component

## 1. Introduction

`motiono` is a React component that simplifies the integration of GreenSock Animation Platform (GSAP) animations into your React applications. It provides a declarative and intuitive way to animate HTML elements, offering a wide range of animation options and flexibility. This documentation provides a comprehensive guide to using `motiono`, covering its features, usage, and advanced techniques.

### 1.1. Core Features

*   **Declarative Animation:** Define animations using props, making your code more readable and maintainable.
*   **GSAP Integration:** Leverages the power and performance of GSAP for smooth and complex animations.
*   **Flexible Animation Types:** Supports `from`, `to`, and `fromTo` animations.
*   **Customizable:** Offers a wide range of animation properties, including duration, delay, easing, repeats, and more.
*   **HTML Element Agnostic:** Works with any HTML element, allowing you to animate various components.
*   **Performance Optimized:** Uses `useRef`, `useMemo`, and `useCallback` hooks to optimize performance and prevent unnecessary re-renders.
*   **Shortcut Components:** Provides memoized shortcut components for common HTML elements (e.g., `motiono.div`, `motiono.span`).
*   **Global Defaults:** Allows setting global defaults for GSAP animations.

### 1.2. Use Cases

*   **Entrance Animations:** Animate elements as they appear on the screen.
*   **Exit Animations:** Animate elements as they disappear.
*   **Interactive Animations:** Create animations triggered by user interactions (e.g., hover, click).
*   **UI Transitions:** Smoothly transition between different UI states.
*   **Complex Animations:** Build sophisticated animations with multiple stages and effects.
*   **Staggered Animations:** Animate multiple elements with a staggered delay.

## 2. Installation

Before using `motiono`, you need to install the necessary dependencies:

```bash
npm install gsap @gsap/react
# or
yarn add gsap @gsap/react
```

## 3. Component Usage

### 3.1. Basic Usage

The `motiono` component is designed to be easy to use. You can animate any HTML element by wrapping it with the `motiono` component and providing animation properties.

```jsx
import React from "react";
import { motiono } from "./motiono"; // Assuming motiono.js is in the same directory

function MyComponent() {
  return (
    <motiono.div
      style={{ width: "100px", height: "100px", backgroundColor: "red" }}
      to={{ x: 200, opacity: 0.5 }}
      duration={2}
    >
      Hello, motiono!
    </motiono.div>
  );
}

export default MyComponent;
```

**Explanation:**

*   `motiono.div`:  Uses the shortcut component for a `div` element.
*   `style`:  Initial inline styles for the animated element.
*   `to`:  Defines the animation's end state.  Here, the element will move 200 pixels to the right (`x: 200`) and become semi-transparent (`opacity: 0.5`).
*   `duration`: Sets the animation duration to 2 seconds.

### 3.2. Animation Types

`motiono` supports three primary animation types:

*   **`from`**: Animates an element *from* a specified state *to* its default state.
*   **`to`**: Animates an element *from* its default state *to* a specified state.
*   **`fromTo`**: Animates an element *from* a specified starting state *to* a specified ending state.

#### 3.2.1. `from` Animation

```jsx
import React from "react";
import { motiono } from "./motiono";

function FromAnimation() {
  return (
    <motiono.div
      style={{ width: "100px", height: "100px", backgroundColor: "blue" }}
      from={{ opacity: 0, x: -100 }} // Start off-screen and transparent
      to={{ opacity: 1, x: 0 }} // Animate to visible and in place
      duration={1}
    >
      From Animation
    </motiono.div>
  );
}

export default FromAnimation;
```

**Explanation:**

*   The element starts with `opacity: 0` (invisible) and `x: -100` (off-screen to the left).
*   The animation moves the element to its default position (`x: 0`) and makes it visible (`opacity: 1`).

#### 3.2.2. `to` Animation

```jsx
import React from "react";
import { motiono } from "./motiono";

function ToAnimation() {
  return (
    <motiono.div
      style={{ width: "100px", height: "100px", backgroundColor: "green" }}
      to={{ scale: 1.5, rotate: 360 }} // Scale up and rotate
      duration={1}
    >
      To Animation
    </motiono.div>
  );
}

export default ToAnimation;
```

**Explanation:**

*   The element starts at its default size and rotation.
*   The animation scales the element to 1.5 times its original size and rotates it 360 degrees.

#### 3.2.3. `fromTo` Animation

```jsx
import React from "react";
import { motiono } from "./motiono";

function FromToAnimation() {
  return (
    <motiono.div
      style={{ width: "100px", height: "100px", backgroundColor: "orange" }}
      fromTo={[{ opacity: 0, y: 50 }, { opacity: 1, y: 0 }]} // Start below and transparent, end in place and visible
      duration={1}
    >
      FromTo Animation
    </motiono.div>
  );
}

export default FromToAnimation;
```

**Explanation:**

*   The element starts below its normal position (`y: 50`) and is transparent (`opacity: 0`).
*   The animation moves the element to its normal position (`y: 0`) and makes it visible (`opacity: 1`).

### 3.3. Animation Properties

`motiono` supports a wide range of animation properties, mirroring the capabilities of GSAP.

## 4. API Reference

The `motiono` component is a wrapper around GSAP's animation capabilities.  It accepts the following props:

### 4.1. `GsapProps` Type Definition

```typescript
/**
 * @typedef {Object} GsapProps
 * @property {string} [tag="div"] - HTML element tag
 * @property {Object} [from] - Starting properties for the animation
 * @property {Object} [to] - Ending properties for the animation
 * @property {[Object, Object]} [fromTo] - Array containing [from, to] properties
 * @property {React.ReactNode} [children] - Child elements
 * @property {string} [className] - CSS class name
 * @property {Object} [style] - Inline CSS styles
 * @property {Function} [onComplete] - Callback when animation completes
 * @property {Function} [onStart] - Callback when animation starts
 * @property {Function} [onUpdate] - Callback during animation updates
 * @property {number} [duration] - Animation duration in seconds
 * @property {number} [delay] - Delay before animation starts
 * @property {boolean} [paused] - Whether animation starts paused
 * @property {number} [repeat] - Number of times to repeat the animation
 * @property {boolean} [yoyo] - Whether animation should reverse on repeat
 * @property {(boolean|string|Function)} [yoyoEase] - Ease for the yoyo phase
 * @property {number} [repeatDelay] - Delay between repeats
 * @property {(string|Function)} [ease] - Animation easing function
 * @property {boolean} [immediateRender] - Whether to render on init
 * @property {(number|Object)} [stagger] - Stagger for animating multiple elements
 * @property {Function} [onTween] - Callback with the tween instance
 */
```

### 4.2. Props Breakdown

*   **`tag` (string, optional, default: `"div"`):**  The HTML element tag to render.  Use this to change the underlying HTML element (e.g., `motiono.span`, `motiono.p`).
*   **`from` (object, optional):**  GSAP properties to animate *from*.  This defines the starting state of the animation.
    *   Example: `{ opacity: 0, x: -100 }`
*   **`to` (object, optional):**  GSAP properties to animate *to*.  This defines the ending state of the animation.
    *   Example: `{ opacity: 1, x: 0 }`
*   **`fromTo` (\[object, object], optional):** An array containing two objects: the `from` and `to` properties.  This is equivalent to using `gsap.fromTo()`.
    *   Example: `[{ opacity: 0, y: 50 }, { opacity: 1, y: 0 }]`
*   **`children` (React.ReactNode, optional):**  The child elements to render within the animated element.
*   **`className` (string, optional):**  CSS class name for the animated element.
*   **`style` (object, optional):**  Inline CSS styles for the animated element.
*   **`onComplete` (function, optional):**  A callback function that is executed when the animation completes.
    *   Example: `() => console.log("Animation complete")`
*   **`onStart` (function, optional):**  A callback function that is executed when the animation starts.
    *   Example: `() => console.log("Animation started")`
*   **`onUpdate` (function, optional):**  A callback function that is executed on every animation update (frame).
    *   Example: `(tween) => console.log("Animation updated", tween.progress())`
*   **`duration` (number, optional, default: `1`):**  The duration of the animation in seconds.
    *   Example: `2` (2 seconds)
*   **`delay` (number, optional, default: `0`):**  The delay before the animation starts, in seconds.
    *   Example: `0.5` (0.5 seconds)
*   **`paused` (boolean, optional, default: `false`):**  Whether the animation should start paused.
    *   Example: `true` (starts paused)
*   **`repeat` (number, optional, default: `0`):**  The number of times to repeat the animation.  `-1` repeats indefinitely.
    *   Example: `2` (repeats twice)
    *   Example: `-1` (repeats infinitely)
*   **`yoyo` (boolean, optional, default: `false`):**  Whether the animation should reverse on each repeat.
    *   Example: `true` (reverses on repeat)
*   **`yoyoEase` (boolean | string | function, optional):** The ease to use for the yoyo phase.  If `true`, it uses the same ease as the
