# Motiono - A React Animation Library Powered by GSAP

**Motiono** is a React library that enables smooth, interactive animations using the power of **GSAP (GreenSock Animation Platform)**. It provides an easy-to-use API for animating React components, offering built-in support for common HTML tags and customizations for a seamless animation experience. Motiono leverages GSAP’s robust capabilities, making it a great choice for handling complex animations in React apps.

This documentation will guide you through the installation, usage, API, and key features of Motiono.

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

To install Motiono, simply run:

```bash
npm install motiono
```

You also need to have `gsap` installed in your project since Motiono leverages GSAP for animations:

```bash
npm install gsap
```

---

## Basic Usage

Once installed, you can import `motiono` and use it to animate any of the built-in tags. Below is an example of animating a `h1` element with a `from` and `to` animation configuration:

### Example:

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
        Hello world
      </motiono.h1>
    </>
  );
}
```

In this example, the `h1` element will animate from the properties defined in `from` to the properties defined in `to` using the specified transition parameters.

---

## Available Tags

Motiono provides an easy way to animate a wide variety of HTML elements by re-exporting built-in React components with animation capabilities. Below are the available tags:

- **Text Tags**: `motiono.h1`, `motiono.h2`, `motiono.h3`, `motiono.h4`, `motiono.h5`, `motiono.h6`, `motiono.p`, `motiono.span`, `motiono.a`
- **Structural Tags**: `motiono.div`, `motiono.section`, `motiono.article`, `motiono.header`, `motiono.footer`, `motiono.nav`, `motiono.main`, `motiono.aside`
- **Form Tags**: `motiono.input`, `motiono.textarea`, `motiono.select`, `motiono.option`, `motiono.label`, `motiono.fieldset`, `motiono.legend`
- **Multimedia Tags**: `motiono.img`, `motiono.video`, `motiono.audio`, `motiono.canvas`, `motiono.iframe`
- **List Tags**: `motiono.ul`, `motiono.ol`, `motiono.li`, `motiono.dl`, `motiono.dt`, `motiono.dd`
- **Other Tags**: `motiono.blockquote`, `motiono.code`, `motiono.pre`, `motiono.em`, `motiono.strong`, `motiono.figure`, `motiono.figcaption`, `motiono.time`, `motiono.details`, `motiono.summary`

---

## API Reference

### motiono Component

The `motiono` component is the core of this library and allows you to animate various HTML elements by passing animation properties.

#### Props

| Prop              | Type                                  | Description                                                                                                                                   |
|-------------------|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `tag`             | `string` (default: `div`)             | HTML tag for the element to animate (e.g., `div`, `span`, `h1`, `section`, etc.).                                                              |
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

This function allows you to set **global GSAP animation defaults** for all animations created via Motiono.

#### Usage:

```js
motiono.setGsapDefaults({
  ease: "power2.out",
  duration: 2,
});
```

This will apply the default easing and duration to all animations unless overridden by individual component settings.

---

## GSAP Integration

Motiono re-exports **GSAP** and **useGSAP** hooks for users who need more advanced control over animations beyond the basic properties. You can access them as follows:

```js
import { gsap, useGSAP } from "motiono";
```

- **gsap**: Direct access to GSAP for more advanced animations.
- **useGSAP**: A custom hook to apply GSAP animations directly within your React components.

### Example with GSAP:

```js
import { useGSAP } from "motiono";
import { gsap } from "gsap";

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

You can chain animations together using GSAP's `timeline`:

```js
const tl = gsap.timeline();
tl.to(".box", { x: 100, duration: 1 });
tl.to(".box", { y: 100, duration: 1 });
```

### Custom Easing Functions

You can create custom easing effects:

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

When using animations in a React app, it’s important to be mindful of the following to maintain good performance:

- **Debounce unnecessary re-renders**: Motiono uses `useMemo` and `useCallback` to optimize rerendering when animation props change.
- **Avoid too many simultaneous animations**: If you animate too many elements simultaneously, it may affect the browser’s performance.
- **Consider using `requestAnimationFrame` for smooth animation rendering**.

---

## Troubleshooting

-
 **Animation not working**: Ensure that the element has the correct reference and that you’ve passed the correct animation properties (`from`, `to`, etc.).
- **Unexpected behavior with `stagger` or `yoyo`**: Double-check your configuration, as conflicting animation properties might cause unexpected results.
- **Performance issues with many animations**: Optimize your animations by reducing the number of active animations or using `gsap.timeline` for better control.

---

This documentation should provide everything you need to get started and make the most of the Motiono library. For more advanced scenarios, refer to the GSAP documentation.
