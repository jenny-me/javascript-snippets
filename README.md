# Javascript Snippets

Collection of frequently used javascript snippets for reference.

- [Observer for animation](#observer-for-animation)
- [Get div behind fixed element](#get-div-behind-fixed-element)
- [Statistic Ticker](#statistic-ticker)
- [Mortage Calculator](#mortgage-calculator)

## Observer for animation

Adds a fade-in animation to all blocks with the `.reveal` class as they become visible to the user. Adding an additional class of `.reveal-left` or `.reveal-right` will shift it in from the side in addition to the fade-in animation.

```js
(function() {  
  const boxElList = document.querySelectorAll(".reveal");
  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.intersectionRatio > 0) {
        entry.target.classList.add("active");
      } 
    });
  });
  
  boxElList.forEach((el) => {
    io.observe(el);
  });
})();
```

The SASS for the animation would look something like:

```sass
.reveal {
  opacity: 0;
  &.active {
    animation: reveal-in .5s .5s ease-out forwards;
  }
  @media all and (min-width: $medium-screen) {
    &.reveal-left {
      &.active {
        animation: reveal-left .5s .5s ease-out forwards;
      }
    }
    &.reveal-right {
      &.active {
        animation: reveal-right .5s .5s ease-out forwards;
      }
    } 
  }
}

@keyframes reveal-in {
  0% {
    opacity: 0;
    transform: translateY(50px);
  }
  100% {
    opacity: 1;
    transform: translateY(0px);
  }
} 
@keyframes reveal-left {
  0% {
    opacity: 0;
    transform: translateX(-50px);
  }
  100% {
    opacity: 1;
    transform: translateY(0px);
  }
} 
@keyframes reveal-right {
  0% {
    opacity: 0;
    transform: translateX(50px);
  }
  100% {
    opacity: 1;
    transform: translateY(0px);
  }
} 
```

## Get div behind fixed element

Function to determine what element is behind a fixed element. Good for state changes based on a fixed navigation or anchor link.

```js
(function() {  
  function getDivBehindFixedElement(fixedElement) {
    // Get the bounding rectangle of the fixed element
    const rect = fixedElement.getBoundingClientRect();

    // Temporarily hide the fixed element
    fixedElement.style.display = 'none';

    // Get the element at the center of the fixed element's position
    const x = rect.left + rect.width / 2;
    const y = rect.top + rect.height / 2;
    const elementBehind = document.elementFromPoint(x, y);

    // Make the fixed element visible again
    fixedElement.style.display = '';

    // If the element behind is a div, return it
    if (elementBehind && elementBehind.tagName.toLowerCase() === 'div') {
        return elementBehind;
    }

    // Otherwise, return null
    return null;
  }
})();
```

## Statistic Ticker

Counts up the number inside the `.countup` class. The script allows for both floats and integers. Also included is an observer to only count up the number when the statistic comes into frame.

[Demo](statistic-ticker.html)

## Mortgage Calculator

Simple mortgage calculator that allows users to change values to see what their costs will be.

[Demo](mortgage-calculator.html)
