---
title: Perfect nested border radius in CSS
language: css
tags: [visual]
cover: rocky-beach-waves
excerpt: Nesting elements with rounded borders can look very wrong if not done correctly. Here's a quick tip on how to do it right.
listed: true
dateModified: 2022-04-03
---

Nesting elements with rounded borders can look very wrong if not done correctly. Luckily, there's a simple math trick to make it look right. All you need to do is **calculate the border radius of one of the elements and the distance between them**.

## The formula

The border radius of the outer element should be equal to the sum of the border radius of the inner element and the distance between the two elements. This can be mathematically expressed as `innerRadius + distance = outerRadius` or more tersely `R1 + D = R2`.

![Nested border radius formula](./illustrations/border-radius.svg)

### Example

Let's take a look at a simple CSS example. Say we want to style two nested boxes with rounded borders. The outer box has a `border-radius` of `24px` and a `padding` of `8px`. Using the previous formula, we can deduce that the inner box should have a `border-radius` of `16px`.

```css
.outer {
  border-radius: 24px;
  padding: 8px;
}

.inner {
  border-radius: 16px;
}
```

## CSS Variables

Using **CSS variables**, we can make this even easier. Depending on the use case, we can adapt the formula to calculate the outer radius from the inner one, or the other way around. Here's an example of how to do this:

<code-tabs>

```css title="From outer radius"
.outer {
  --outer-radius: 24px;
  --padding: 8px;
  --inner-radius: calc(var(--outer-radius) - var(--padding));

  border-radius: var(--outer-radius);
  padding: var(--padding);
}

.inner {
  border-radius: var(--inner-radius);
}
```

```css title="From inner radius"
.outer {
  --inner-radius: 16px;
  --padding: 8px;
  --outer-radius: calc(var(--inner-radius) + var(--padding));

  border-radius: var(--outer-radius);
  padding: var(--padding);
}

.inner {
  border-radius: var(--inner-radius);
}
```

</code-tabs>

> [!NOTE]
>
> This setup may work for simple cases, but if you have multiple `padding` or `margin` values, you may need to tweak it to fit your needs.
