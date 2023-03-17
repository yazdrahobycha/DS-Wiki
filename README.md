# Side-Menu Info Site for Kottans

This is a solution to the "Document Object Model" task by [Kottans](https://github.com/kottans).

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Code Highlights](#code-highlights)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

## Overview

### The challenge

Users should:

- Be able to load predetermined content into the `<main>` container when a tab is clicked
- Have the ability to switch between tabs to view loaded content
- See hover and focus states of interactive elements
- Be able to switch between tabs using the tab key
- See an optimal layout for their device screen size
- Have the ability to see the active tab's state.

### Screenshot

<p align="center">
  <img src="img/DS-wiki Demo.png" alt="Project Photo"/>
</p>

### Links

[Demo](https://soft-malasada-c2cfcf.netlify.app/) | [Pull-Request](https://github.com/kottans/frontend-2019-p2p/pull/222)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- Vanilla JavaScript
- the DOM
- Visual Studio Code
- Netlify
- Tested in Google Chrome, Mozilla Firefox, Safari

This code was built using standard web technologies and does not rely on any third-party libraries or frameworks.

### What I learned

This project was my first experience in manipulating the DOM tree, which, of course, was both inspiring and intimidating at the same time! During its implementation, I encountered numerous issues in implementing my ideas, particularly from the JavaScript side, since it was my first time working with them. A lot of time was spent developing the logic through which I could create HTML content for the `<main>` element within the JavaScript itself and connect the relevant tabs with content loading.

Overall, while working with this project, I learned the importance of properly naming variables and functions to make the code more readable and easier to maintain. I also learned the value of testing the code thoroughly to catch any bugs or errors that may arise.

### Code Highlights

The JavaScript script is designed to create a navigation menu, handle user input, and display information about different topics on an HTML page. The code uses basic JavaScript concepts such as functions, variables, conditionals, and event listeners.

<details>
<summary>Function that creates a menu with clickable links based on an array of article titles.</summary>

```javascript
function makeMenu(allArticles) {
    const [header, ...navLinks] = allArticles.map(({ title }, index) => {
        return index === 0
            ? `<h1 data-number="0" tabindex="0" class="menu_title">${title}</h1>`
            : `<li class="menu_item" data-number="${index}" tabindex="0">${title}</li>`;
    });
    elements.$header.insertAdjacentHTML('beforeend', header);
    elements.$nav.insertAdjacentHTML(
        'afterbegin',
        `<ul class="menu">${navLinks.join(' ')}</ul>`
    );
}
```

</details>

<details>
<summary>handling user input and creating/displaing appropriate information</summary>

```javascript
function selectInfoItem(event) {
    if (
        event.type === 'keydown' &&
        event.code !== 'Space' &&
        event.code !== 'Enter'
    ) {
        return;
    }
    event.preventDefault();
    const { target } = event;
    if (target.closest('.menu_item, .menu_title')) {
        elements.$main.innerHTML = '';
        elements.$body.scrollTo(0, 0);
        createAndShowInfoItem(
            elements.$main,
            articlesInfo,
            Number(target.dataset.number)
        );
        if (target.closest('.active')) {
            toggleMenu();
        }
    } else if (target.closest('.navigation.active')) {
        toggleMenu();
    }
}
```

```javascript
function createAndShowInfoItem($container, articlesArr, index = 0) {
    changeActiveLink(index);
    const { title, text } = articlesArr[index];
    const snakeTitle = toSnakeCase(title);
    const insertContent = `<div class="text_container">${paragraphsSplit(
        text
    )}</div>
    <img class="${snakeTitle} content_img" src="img/${snakeTitle}.png">`;
    $container.insertAdjacentHTML('afterbegin', insertContent);
    if (index !== 0) {
        $container.insertAdjacentHTML(
            'afterbegin',
            `<h2 class="content_title">${title}</h2>`
        );
    }
}
```

</details>

### Continued development

- **Responsive Design:** Currently, the code is not fully optimized for mobile or tablet devices. Adding responsive design would make the website accessible to a wider range of users.
- **Accessibility:** While the code includes some basic accessibility features like keyboard navigation and focus outlines, there are still many areas where it could be improved to meet modern accessibility standards.
- **Additional Features:** The current website is relatively simple and could benefit from additional features or functionality, such as animations, search functionality, or social media integration.
- **Code Optimization:** The code could be further optimized to improve its performance and load times, which would provide a better user experience and help the website rank better in search engines.

### Useful resources

- [Фрілансер по життю: Адаптивний Шрифт](https://www.youtube.com/watch?v=HJZP5QsrpXs&t=591s) - Great video about adaptive fonts styling.
- [Фрілансер по життю: JavaScript События](https://www.youtube.com/watch?v=bWCzbR5DvCo&t=1281s) - Great video about adaptive fonts styling.
- [CSS Bud glow generator](https://cssbud.com/css-generator/css-glow-generator/) - Great generator of neon-glove effects
- [The Fixed Background Attachment Hack](https://css-tricks.com/the-fixed-background-attachment-hack/) - Great article about solution of 'fixed background' on the mobiles problem

## Author

- Instagram - [@yazdrahobycha](https://instagram.com/yazdrahobycha?igshid=YmMyMTA2M2Y=)
- Telegram - [Орсен](https://t.me/yazdrahobb)

## Acknowledgments

Big thanks to [Igor4ik](https://github.com/bigheha) for support!
