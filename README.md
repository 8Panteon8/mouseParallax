# Mouse parallax

Great parallax effect for your website header. The effect works on both mouse and scrolling.


## Key parts

- **Style additions**

```javascript
function setMouseParallaxStyle() {
      const distX = coordXprocent - positionX;
      const distY = coordYprocent - positionY;

      positionX = positionX + distX * speed;
      positionY = positionY + distY * speed;

      // Style Transfer
      clouds.style.cssText = `transform: translate(${positionX / forClouds}%, ${
        positionY / forClouds
      }%);`;
      mountains.style.cssText = `transform: translate(${
        positionX / forMountains
      }%, ${positionY / forMountains}%);`;
      human.style.cssText = `transform: translate(${positionX / forHuman}%, ${
        positionY / forHuman
      }%);`;

      requestAnimationFrame(setMouseParallaxStyle);
    }
```

- **Calculating mouse position**

```javascript
parallax.addEventListener("mousemove", function (e) {
      const parallaxWidth = parallax.offsetWidth;
      const parallaxHeight = parallax.offsetHeight;

      const coordX = e.pageX - parallaxWidth / 2;
      const coordY = e.pageY - parallaxHeight / 2;

      coordXprocent = (coordX / parallaxWidth) * 100;
      coordYprocent = (coordY / parallaxHeight) * 100;
    });
```

- **Parallax scrolling**


```javascript
let thresholdSets = [];
for (let i = 0; i <= 1.0; i += 0.005) {
  thresholdSets.push(i);
}

const callback = function (entries, observer) {
  const scrollTopProcent =
    (window.pageYOffset / parallax.offsetHeight) * 100;
  setParallaxItemsStyle(scrollTopProcent);
};
const observer = new IntersectionObserver(callback, {
  threshold: thresholdSets,
});

observer.observe(document.querySelector(".content"));

function setParallaxItemsStyle(scrollTopProcent) {
  content.style.cssText = `transform: translate(0% ,-${
    scrollTopProcent / 9
  }%);`;
  mountains.parentElement.style.cssText = `transform: translate(0% ,-${
    scrollTopProcent / 9
  }%);`;
  human.parentElement.style.cssText = `transform: translate(0% ,-${
    scrollTopProcent / 3
  }%);`;
```

- **Gradient was added to soften the transition**

```css
.content::before {
  pointer-events: none;
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 300px;
  transform: translate(0px, -100%);
  background: linear-gradient(180deg, rgba(11, 29, 38, 0) 5%, #0b1d26 100%);
}
```

## Screenshot

![ezgif com-video-to-gif](https://user-images.githubusercontent.com/113831614/224319221-da4f5842-7eef-4cba-9328-672fed97d8fd.gif)

