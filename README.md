# Motiono - A React Animation Library Powered by GSAP

**Motiono** is a React library that simplifies creating smooth, interactive animations by leveraging **GSAP (GreenSock Animation Platform)**. It provides a clean, declarative API for animating React components, giving developers the flexibility to animate built-in HTML elements and custom React components. With built-in GSAP integration, Motiono makes creating sophisticated animations easy without any external setup.

This documentation will guide you through the installation, basic usage, available tags, API references, advanced usage, performance tips, and troubleshooting.

---

## Table of Contents
- [Installation](#installation)
- [Basic Usage](#basic-usage)
- [Available Tags](#available-tags)
- [API Reference](#api-reference)
  - [motiono Component](#motiono-component)
  - [motiono.setGsapDefaults](#motionosetgsapdefaults)
  - [GSAP Integration](#gsap-integration)
- [Advanced Usage](#advanced-usage)
- [Performance Considerations](#performance-considerations)
- [Troubleshooting](#troubleshooting)

---

## Installation

You can install **Motiono** via npm:

```bash
npm install motiono
```

---

## Basic Usage

Motiono makes it simple to animate HTML elements. Once installed, import `motiono` into your React components and animate tags like you would with any standard HTML element.

### Example: Animate a Heading (`h1`)

```js
import { motiono } from "motiono";

export default function App() {
  return (
    <>
      <motiono.h1
        from={{ scale: 0.3, y: -150, rotate: -15, opacity: 0 }}
        to={{ scale: 1, y: 0, rotate: 0, opacity: 1 }}
        transition={{
          type: "spring",
          stiffness: 700,
          damping: 10,
          mass: 1.5,
        }}
        style={{
          fontSize: "4rem",
          textAlign: "center",
          marginTop: "3rem",
          fontWeight: "bold",
        }}
      >
        Hello World
      </motiono.h1>
    </>
  );
}
```

In this example, the `h1` element will animate from the defined `from` properties (small scale, offscreen, rotated) to the `to` properties (full scale, centered, no rotation). You can customize the animation using `transition` properties such as easing, stiffness, and damping.

---

## Available Tags

Motiono supports a wide range of HTML tags that you can animate out of the box. These include:

- **Text Tags**: `motiono.h1`, `motiono.h2`, `motiono.h3`, `motiono.h4`, `motiono.h5`, `motiono.h6`, `motiono.p`, `motiono.span`, `motiono.a`
- **Structural Tags**: `motiono.div`, `motiono.section`, `motiono.article`, `motiono.header`, `motiono.footer`, `motiono.nav`, `motiono.main`, `motiono.aside`
- **Form Tags**: `motiono.input`, `motiono.textarea`, `motiono.select`, `motiono.option`, `motiono.label`, `motiono.fieldset`, `motiono.legend`
- **Multimedia Tags**: `motiono.img`, `motiono.video`, `motiono.audio`, `motiono.canvas`, `motiono.iframe`
- **List Tags**: `motiono.ul`, `motiono.ol`, `motiono.li`, `motiono.dl`, `motiono.dt`, `motiono.dd`
- **Other Tags**: `motiono.blockquote`, `motiono.code`, `motiono.pre`, `motiono.em`, `motiono.strong`, `motiono.figure`, `motiono.figcaption`, `motiono.time`, `motiono.details`, `motiono.summary`

---

## API Reference

### motiono Component

The `motiono` component is the main entry point for creating animations in Motiono. It provides a simple and declarative interface for animating various HTML elements.

#### Props

| Prop              | Type                                  | Description                                                                                                                                   |
|-------------------|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `tag`             | `string` (default: `div`)             | The HTML tag to animate (e.g., `div`, `span`, `h1`).                                                                                          |
| `from`            | `Object`                              | The starting properties for the animation (e.g., `{ scale: 0.5, y: -200, opacity: 0 }`).                                                        |
| `to`              | `Object`                              | The ending properties for the animation (e.g., `{ scale: 1, y: 0, opacity: 1 }`).                                                              |
| `fromTo`          | `Array` (`[from, to]`)                | An array of two objects, defining both starting and ending animation properties.                                                               |
| `children`        | `React.ReactNode`                     | The content or child elements inside the animated component.                                                                                   |
| `className`       | `string`                              | CSS class name to apply to the element.                                                                                                        |
| `style`           | `Object`                              | Inline CSS styles for the element.                                                                                                             |
| `onComplete`      | `Function`                            | Callback fired when the animation completes.                                                                                                    |
| `onStart`         | `Function`                            | Callback fired when the animation starts.                                                                                                      |
| `onUpdate`        | `Function`                            | Callback fired on each update during the animation.                                                                                             |
| `duration`        | `number` (default: `1`)               | Duration of the animation in seconds.                                                                                                          |
| `delay`           | `number`                              | Delay before the animation starts.                                                                                                             |
| `paused`          | `boolean` (default: `false`)          | Whether the animation starts paused.                                                                                                           |
| `repeat`          | `number`                              | The number of times to repeat the animation.                                                                                                   |
| `yoyo`            | `boolean`                              | Whether the animation should reverse on repeat.                                                                                                |
| `yoyoEase`        | `boolean | string | Function`         | The easing function for the yoyo phase.                                                                                                        |
| `ease`            | `string | Function`                  | The easing function for the animation (e.g., `"power1.out"`, `"ease-in"`, etc.).                                                               |
| `immediateRender` | `boolean` (default: `false`)          | Whether to render the element immediately or wait for the animation.                                                                            |
| `stagger`         | `number | Object`                     | The stagger effect for animating multiple elements.                                                                                            |
| `onTween`         | `Function`                            | Callback that provides the tween instance for further manipulation.                                                                            |

#### Example:

```js
<motiono.div
  from={{ opacity: 0 }}
  to={{ opacity: 1 }}
  duration={2}
  ease="easeOutQuad"
  onComplete={() => console.log("Animation Complete")}
>
  <p>This is an animated div!</p>
</motiono.div>
```

### motiono.setGsapDefaults

This function allows you to set global GSAP animation defaults for all animations created via Motiono. You can apply settings like default easing and duration across your app without specifying them in every animation.

#### Usage:

```js
motiono.setGsapDefaults({
  ease: "power2.out",
  duration: 2,
});
```

---

## GSAP Integration

Motiono integrates GSAP by default. You do not need to import GSAP separately unless you want more advanced control. This gives you the ability to use GSAP's full power when needed, but you can still create smooth animations using the declarative syntax.

- **GSAP**: Directly accessible for advanced animation logic.
- **useGSAP**: A custom hook to apply GSAP animations directly within your React components.

### Example with GSAP:

```js
import { useGSAP } from "motiono";
import { gsap } from "motiono";

function App() {
  const ref = useRef(null);

  useGSAP(() => {
    gsap.to(ref.current, { x: 200, duration: 1 });
  });

  return <div ref={ref}>This element will move</div>;
}
```

---

## Advanced Usage

### Animation Chaining

You can chain animations using GSAP's `timeline` API for more complex sequences:

```js
const tl = gsap.timeline();
tl.to(".box", { x: 100, duration: 1 });
tl.to(".box", { y: 100, duration: 1 });
```

### Custom Easing Functions

Motiono supports custom easing functions through GSAP:

```js
import { gsap } from "gsap";

gsap.to(".box", {
  x: 500,
  duration: 2,
  ease: "elastic.out(1, 0.75)",
});
```

---

## Performance Considerations

To ensure good performance when using animations in a React app, keep the following points in mind:

- **Debounce re-renders**: Motiono uses hooks like `useMemo` and `useCallback` to minimize unnecessary renders.
- **Limit simultaneous animations**: Excessive simultaneous animations can degrade performance, so optimize accordingly.
- **Use `requestAnimationFrame` for smooth rendering**: This is automatically handled by GSAP, but make sure you're not overwriting it in your animations.

---

## Troubleshooting

- **Animation not triggering**: Double-check the element's
 reference and ensure `from` and `to` properties are properly defined.
- **Unexpected results with `stagger` or `yoyo`**: Inspect your configuration for conflicting animation properties.
- **Performance issues**: Optimize animations by reducing the number of concurrent active animations or using `gsap.timeline()` for grouped animations.

---

Motiono simplifies animation workflows in React by providing a default GSAP integration and an intuitive API for developers to create beautiful, performance-optimized animations with ease.
