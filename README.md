# Fabric.js

<a href="http://fabricjs.com/kitchensink" target="_blank"><img align="right" src="/lib/screenshot.png" width="400"></a>

A **simple and powerful Javascript HTML5 canvas library**.

- [**Website**][website]
- [**Old V5 documentation**](https://fabric5.fabricjs.com)
- [**GOTCHAS**][gotchas]
- [**Contributing, Developing and More**](CONTRIBUTING.md)

## Special Thanks

Here is a section for recognition of companies or individuals that support fabricJS with a sponsorship

   <a href="https://go.warp.dev/fabric">
      <img alt="Warp sponsorship" width="300" src="https://github.com/warpdotdev/brand-assets/blob/main/Github/Sponsor/Warp-Github-LG-01.png">
   </a>

### [Warp, built for coding with multiple AI agents](https://go.warp.dev/fabric)

[Available for MacOS, Linux, & Windows](https://go.warp.dev/fabric)<br>

</div>

## Features

- Out of the box interactions such as scale, move, rotate, skew, group...
- Built in shapes, controls, animations, image filters, gradients, patterns, brushes...
- `JPG`, `PNG`, `JSON` and `SVG` i/o
- Typed and modular
- [Unit tested](CONTRIBUTING.md#-testing)

#### Supported Browsers/Environments

|   Context   | Supported Version | Notes                           |
| :---------: | :---------------: | ------------------------------- |
|   Firefox   |        ✔️         | 58                              |
|   Safari    |        ✔️         | 11                              |
|    Opera    |        ✔️         | chromium based                  |
|   Chrome    |        ✔️         | 64                              |
|    Edge     |        ✔️         | chromium based                  |
| Edge Legacy |        ❌         |
|    IE11     |        ❌         |
|   Node.js   |        ✔️         | [Node.js installation](#nodejs) |

Fabric.js does not use polyfills by default, or tries to keep it at minimum. the browser version we support is determined by the level of canvas api we want to use and some js syntax. While JS can be easily transpiled, canvas API can't.

## Installation

```bash
$ npm install fabric --save
# or use yarn
$ yarn add fabric
# or use pnpm
$ pnpm install fabric
```

#### Browser

[![cdnjs](https://img.shields.io/cdnjs/v/fabric.js.svg)][cdnjs]
[![jsdelivr](https://data.jsdelivr.com/v1/package/npm/fabric/badge)][jsdelivr]

See [browser modules][mdn_es6] for using es6 imports in the browser or use a dedicated bundler.

#### Node.js

We strongly recommend to run your applications only LTS versions of node.

Said so the minimum supported version of node is 18.
We bump up the minimum version of node with a Major release only when the dependencies force us to do so.

Fabric.js depends on [node-canvas][node_canvas] for a canvas implementation (`HTMLCanvasElement` replacement) and [jsdom][jsdom] for a `window` implementation on node.
This means that you may encounter `node-canvas` limitations and [bugs][node_canvas_issues].

Follow these [instructions][node_canvas_install] to get `node-canvas` up and running.

## Quick Start

```js
// v6
import { Canvas, Rect } from 'fabric'; // browser
import { StaticCanvas, Rect } from 'fabric/node'; // node

// v5
import { fabric } from 'fabric';
```

<details><summary><b>Plain HTML</b></summary>

```html
<canvas id="canvas" width="300" height="300"></canvas>

<script src="https://cdn.jsdelivr.net/npm/fabric@6.4.3/dist/index.js"></script>
<script>
  const canvas = new fabric.Canvas('canvas');
  const rect = new fabric.Rect({
    top: 100,
    left: 100,
    width: 60,
    height: 70,
    fill: 'red',
  });
  canvas.add(rect);
</script>
```

</details>

<details><summary><b>React.js</b></summary>

```tsx
import React, { useEffect, useRef } from 'react';
import * as fabric from 'fabric'; // v6
import { fabric } from 'fabric'; // v5

export const FabricJSCanvas = () => {
  const canvasEl = useRef<HTMLCanvasElement>(null);
  useEffect(() => {
    const options = { ... };
    const canvas = new fabric.Canvas(canvasEl.current, options);
    // make the fabric.Canvas instance available to your app
    updateCanvasContext(canvas);
    return () => {
      updateCanvasContext(null);
      canvas.dispose();
    }
  }, []);

  return <canvas width="300" height="300" ref={canvasEl}/>;
};

```

</details>

<details><summary><b>Node.js</b></summary>

```js
import http from 'http';
import * as fabric from 'fabric/node'; // v6
import { fabric } from 'fabric'; // v5

const port = 8080;

http
  .createServer((req, res) => {
    const canvas = new fabric.Canvas(null, { width: 100, height: 100 });
    const rect = new fabric.Rect({ width: 20, height: 50, fill: '#ff0000' });
    const text = new fabric.Text('fabric.js', { fill: 'blue', fontSize: 24 });
    canvas.add(rect, text);
    canvas.renderAll();
    if (req.url === '/download') {
      res.setHeader('Content-Type', 'image/png');
      res.setHeader('Content-Disposition', 'attachment; filename="fabric.png"');
      canvas.createPNGStream().pipe(res);
    } else if (req.url === '/view') {
      canvas.createPNGStream().pipe(res);
    } else {
      const imageData = canvas.toDataURL();
      res.writeHead(200, '', { 'Content-Type': 'text/html' });
      res.write(`<img src="${imageData}" />`);
      res.end();
    }
  })
  .listen(port, (err) => {
    if (err) throw err;
    console.log(
      `> Ready on http://localhost:${port}, http://localhost:${port}/view, http://localhost:${port}/download`,
    );
  });
```

</details>

See our ready to use [templates](./.codesandbox/templates/).

---

## Other Solutions

| Project                        | Description          |
| ------------------------------ | -------------------- |
| [Three.js][three.js]           | 3D graphics          |
| [PixiJS][pixijs]               | WebGL renderer       |
| [Konva][konva]                 | Similar features     |
| [html-to-image][html-to-image] | HTML to image/canvas |

## More Resources

- [WIP new fabricjs.com](https://fabricjs.github.io)
- [Demos on `fabricjs.com`][demos]
- [Fabric.js on `Twitter`][twitter]
- [Fabric.js on `CodeTriage`][code_triage]
- [Fabric.js on `Stack Overflow`][so]
- [Fabric.js on `jsfiddle`][jsfiddles]
- [Fabric.js on `Codepen.io`][codepens]

## Credits [![Patreon](https://img.shields.io/static/v1?label=Patreon&message=%F0%9F%91%8D&logo=Patreon&color=blueviolet)](https://www.patreon.com/fabricJS)

- [kangax][kagnax]
- [asturur][asturur] on [`Twitter`][asturur_twitter]
  [![Sponsor asturur](https://img.shields.io/static/v1?label=Sponsor%20asturur&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86)](https://github.com/sponsors/asturur)
- [ShaMan123][shaman123] [![Sponsor ShaMan123](https://img.shields.io/static/v1?label=Sponsor%20ShaMan123&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86)](https://github.com/sponsors/ShaMan123)
- [melchiar][melchiar] [![Sponsor melchiar](https://img.shields.io/static/v1?label=Sponsor%20melchiar&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86)](https://github.com/sponsors/melchiar)
- Ernest Delgado for the original idea of [manipulating images on canvas](http://www.ernestdelgado.com/archive/canvas/)
- [Maxim "hakunin" Chernyak](http://twitter.com/hakunin) for ideas, and help with various parts of the library throughout its life
- [Sergey Nisnevich](http://nisnya.com) for help with geometry logic
- [Stefan Kienzle](https://twitter.com/kienzle_s) for help with bugs, features, documentation, GitHub issues
- [Shutterstock](http://www.shutterstock.com/jobs) for the time and resources invested in using and improving Fabric.js
- [and all the other contributors][contributors]

[asturur]: https://github.com/asturur
[asturur_twitter]: https://twitter.com/AndreaBogazzi
[cdnjs]: https://cdnjs.com/libraries/fabric.js
[code_triage]: https://www.codetriage.com/kangax/fabric.js
[codepens]: https://codepen.io/tag/fabricjs
[contributors]: https://github.com/fabricjs/fabric.js/graphs/contributors
[demos]: http://fabricjs.com/demos/
[gotchas]: https://fabricjs.com/docs/old-docs/gotchas/
[html-to-image]: https://github.com/bubkoo/html-to-image
[jsdelivr]: https://www.jsdelivr.com/package/npm/fabric
[jsdom]: https://github.com/jsdom/jsdom
[jsfiddles]: https://jsfiddle.net/user/fabricjs/fiddles/
[kagnax]: https://twitter.com/kangax
[konva]: https://github.com/konvajs/konva
[mdn_es6]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules
[melchiar]: https://github.com/melchiar
[node_canvas]: https://github.com/Automattic/node-canvas
[node_canvas_install]: https://github.com/Automattic/node-canvas#compiling
[node_canvas_issues]: https://github.com/Automattic/node-canvas/issues
[patreon_badge]: https://img.shields.io/static/v1?label=Patreon&message=%F0%9F%91%8D&logo=Patreon&color=blueviolet
[pixijs]: https://github.com/pixijs/pixijs
[shaman123]: https://github.com/ShaMan123
[so]: https://stackoverflow.com/questions/tagged/fabricjs
[three.js]: https://github.com/mrdoob/three.js/
[twitter]: https://twitter.com/fabricjs
[website]: http://fabricjs.com/

19.02.26 synk fork
Ось результати аналізу та стратегія трансформації для проекту **Fabric.js**, підготовлені у форматі для копіювання в Notion.

---

# 📑 Звіт AI-консультанта: Проект "Fabric.js"

**Fabric.js** — це потужна та проста бібліотека для роботи з HTML5 Canvas на JavaScript, яка також включає парсер SVG-to-Canvas та Canvas-to-SVG.

---

## 🧬 Частина 1: "ДНК" Проекту

Логіку коду проекту можна розбити на такі **атомарні функції**:

*   **Маніпуляція об'єктами:** Функції для масштабування, переміщення, обертання, нахилу та групування об'єктів безпосередньо на полотні.
*   **Парсинг та Серіалізація:** Вбудована підтримка імпорту та експорту даних у форматах **SVG, JSON, JPG та PNG**.
*   **Рендеринг та Візуалізація:** Робота з вбудованими фігурами, елементами керування, анімаціями, градієнтами та паттернами.
*   **Обробка подій та взаємодія:** Готові механізми взаємодії з користувачем ("out of the box interactions").
*   **Обробка медіа:** Застосування фільтрів до зображень та робота з пензлями для малювання.
*   **Крос-платформна підтримка:** Можливість роботи як у браузері, так і в середовищі **Node.js** (з використанням node-canvas та jsdom).

### 💎 Головна технічна цінність
Головна цінність Fabric.js полягає в наданні **інтерактивної об'єктної моделі поверх HTML5 Canvas**. Замість малювання окремих пікселів, розробник працює з "живими" об'єктами, які мають стан, властивості та здатність до взаємодії, що критично для створення графічних редакторів та інтерактивних веб-додатків.

---

## 🚀 Частина 2: "Трансформація" (Інтеграція з Gemini LLM)

Додавання мультимодальної моделі **Gemini** (через **GitHub Models**) перетворює Fabric.js із графічного рушія на **автономного ШІ-дизайнера**.

### Як зміниться функціонал?
1.  **Генеративний дизайн (Prompt-to-Canvas):** Користувач описує бажану композицію природною мовою, а Gemini генерує складний JSON-об'єкт, який Fabric.js миттєво відмальовує на полотні.
2.  **Інтелектуальне редагування:** ШІ може аналізувати поточні об'єкти на полотні та пропонувати покращення (наприклад: *"Зроби кольори більш гармонійними"* або *"Вирівняй усі логотипи за сіткою"*).
3.  **Автоматична векторизація та опис:** Gemini може приймати скріншот полотна, описувати його вміст або перетворювати растрові начерки користувача у правильні геометричні форми Fabric.js.

### Сценарій сервісу "AI Creative Studio" (Fabric.js + Gemini + ID_{$})

Створення сервісу інтелектуального створення графіки на вашому сайті:
1.  **Запит користувача:** Користувач вводить текст: *"Створи банер для кав'ярні у мінімалістичному стилі"*.
2.  **Інтелект (Gemini):** Модель (через **GitHub Models**) формує структуру дизайну (фігури, кольори, тексти) у форматі JSON, сумісному з Fabric.js.
3.  **Логіка обробки (ID_{$}):** Ваш Python-скрипт **ID_{$}** отримує цей JSON, валідує його та додає ваші фірмові елементи (логотипи, шрифти) з бази даних.
4.  **Візуалізація (Fabric.js):** На фронтенді Fabric.js отримує фінальний JSON і відображає інтерактивний макет, де користувач може вручну підкоригувати деталі.
5.  **Експорт (ID_{$}):** Після завершення інший Python-скрипт **ID_{$}** використовує Fabric.js на стороні сервера (Node.js) для рендерингу фінального зображення у високій якості та його збереження.
6.  **Деплой:** Використовуючи **GitHub Spark**, ви розгортаєте цей інтелектуальний інтерфейс як готовий сервіс.

---

## 📋 План дій для Notion
| Крок | Дія | Результат |
| :--- | :--- | :--- |
| **1** | Встановлення: `npm install fabric` | Базова бібліотека в проекті |
| **2** | Підключення Gemini через **GitHub Models** | "Мізки" для генерації дизайну |
| **3** | Створення API-містка між Python **ID_{$}** та JS | Обмін даними дизайну (JSON/SVG) |
| **4** | Розгортання фронтенду через **GitHub Spark** | Готовий сервіс для користувачів |

---

### 💡 Резюме

**Суть:** **Бібліотека для інтерактивної роботи з полотном (Canvas)**.

**AI-Роль:** **Побудова інтелектуальних застосунків через Spark**.
