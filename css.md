Let's break down your CSS code line by line, explaining the underlying concepts and best practices along the way. This is your design and styling blueprint for the HTML structure we discussed earlier.

---

### **Understanding CSS Basics**

- **What is CSS?** CSS (Cascading Style Sheets) is a stylesheet language used to describe the presentation of a document written in HTML (or XML). It dictates how elements should be rendered on screen, on paper, in speech, or on other media.
- **How does it work?** CSS works by applying rules to HTML elements. Each rule consists of a:
  - **Selector:** Specifies which HTML elements the rule applies to (e.g., `body`, `.navbar`, `#contact`).
  - **Declaration Block:** Contains one or more declarations, enclosed in curly braces `{}`.
  - **Declaration:** A property-value pair (e.g., `color: #333;`).
    - **Property:** The aspect of the element you want to change (e.g., `font-family`, `margin`, `background-color`).
    - **Value:** The specific setting for that property (e.g., `"Poppins", sans-serif`, `1rem auto`, `#fc036b`).
- **Cascading:** This is a core concept. When multiple CSS rules apply to the same element, the browser determines which rule "wins" based on:
  1.  **Specificity:** More specific selectors override less specific ones.
  2.  **Order of Appearance:** If specificity is equal, the last rule declared wins.
  3.  **Importance:** `!important` overrides everything (use sparingly).

---

### **Line-by-Line CSS Explanation**

```css
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap");
```

- `@import url(...)`: This is an **at-rule** that allows you to import one CSS stylesheet into another.
  - **Concept:** While `<link>` in HTML is generally preferred for performance (as it allows parallel downloading and rendering), `@import` can be used to consolidate CSS files or import resources like fonts.
  - **In Detail:** Here, you're importing the Poppins font from Google Fonts. This line is functionally similar to the `<link>` tag in your HTML head for Google Fonts. For production, the `<link>` tag directly in HTML is usually better because it doesn't block parallel downloads of other resources, but for simplicity or specific bundling, `@import` can be used.

---

### **Base Styles & Resets (`/* --- Base Styles & Resets --- */`)**

These rules target fundamental HTML elements to provide a consistent starting point across different browsers, as browsers often have default styles that can vary.

```css
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

- `*`: The **universal selector**. It selects _all_ elements in the HTML document.
- `*::before`, `*::after`: These are **pseudo-elements**. They refer to generated content before or after an element's content.
  - **Concept:** Used primarily for decorative purposes (like icons or clever layout tricks) or to add content that isn't directly in the HTML.
- `margin: 0;`: Removes default outer spacing (margin) from all elements.
- `padding: 0;`: Removes default inner spacing (padding) from all elements.
- `box-sizing: border-box;`: This is a fundamental CSS reset for layout.
  - **Concept:** Controls how the total width and height of an element are calculated.
  - **In Detail:**
    - By default (`content-box`), the `width` and `height` properties only refer to the content area. Padding and border are _added_ to this, making the element larger than its specified width/height.
    - `border-box` includes padding and border _within_ the specified `width` and `height`. This makes layout calculations much more intuitive because an element's declared `width` (e.g., `width: 100px;`) will always be its actual rendered width, regardless of padding or border. This is a best practice for modern CSS layouts.

<!-- end list -->

```css
html {
  scroll-behavior: smooth;
  font-size: 1rem; /* Base font size for rem units (16px) */
}
```

- `html`: Selects the root `<html>` element.
- `scroll-behavior: smooth;`:
  - **Concept:** When a user clicks on an anchor link (e.g., `href="#sectionId"`), this property makes the browser smoothly scroll to the target element instead of abruptly jumping.
  - **In Detail:** This provides a better user experience for in-page navigation. It's a CSS-only solution, replacing the need for JavaScript for simple smooth scrolling.
- `font-size: 1rem;`: Sets the base font size for the entire document.
  - **Concept:** `rem` (root em) units are relative to the `font-size` of the `<html>` element. If `html` is `1rem` (which typically defaults to `16px` in most browsers), then `1rem` elsewhere equals `16px`.
  - **In Detail:** Using `rem` units for font sizes and spacing (margins, padding) is a best practice for **scalability and accessibility**. If a user changes their browser's default font size (or if you change the `html`'s `font-size`), all `rem` units scale proportionally, ensuring your layout remains coherent. This is generally preferred over `px` for font sizes for accessibility reasons.

<!-- end list -->

```css
body {
  font-family: "Poppins", sans-serif;
  line-height: 1.6;
  color: #333;
  overflow-x: hidden; /* Prevents horizontal scroll from mobile menu */
}
```

- `body`: Selects the `<body>` element.
- `font-family: "Poppins", sans-serif;`: Sets the preferred font for the entire body text.
  - **Concept:** Specifies a prioritized list of font families. The browser will try to use "Poppins" first. If it's not available (or doesn't load), it falls back to a generic `sans-serif` font (like Arial, Helvetica), ensuring text is always readable.
- `line-height: 1.6;`: Sets the height of each line of text relative to its font size.
  - **Concept:** `1.6` means the line height is 1.6 times the current font size (e.g., if font size is 16px, line height is 16 \* 1.6 = 25.6px).
  - **In Detail:** A `line-height` without units (like `1.6` instead of `1.6rem` or `160%`) is often preferred because it calculates the line height relative to the _element's own font size_, which is more scalable. Good line height improves readability.
- `color: #333;`: Sets the default text color to a dark gray.
  - **Concept:** `color` property sets the foreground color of an element's text content. Hex codes (`#333`) are a common way to specify colors.
- `overflow-x: hidden;`:
  - **Concept:** Controls what happens to content that overflows the element's box horizontally.
  - **In Detail:** Setting it to `hidden` prevents a horizontal scrollbar from appearing if content (like your off-screen mobile navigation menu) extends beyond the viewport width. This is important for a clean user experience on mobile.

<!-- end list -->

```css
a {
  text-decoration: none;
  color: inherit; /* Inherit color unless explicitly set */
}
```

- `a`: Selects all anchor `<a>` elements (links).
- `text-decoration: none;`: Removes the default underline from links.
- `color: inherit;`: Links will inherit their text color from their parent element.
  - **Concept:** `inherit` is a keyword that tells a property to take the computed value of its parent element.
  - **In Detail:** This is a good reset, as links often have a distinct blue color by default. By inheriting, they start with the `body` color (`#333`) and you can then explicitly style `navbar__nav-link` or `button` colors later.

<!-- end list -->

```css
ul {
  list-style: none;
}
```

- `ul`: Selects all unordered list `<ul>` elements.
- `list-style: none;`: Removes the default bullet points (or other list markers) from unordered lists.
  - **Concept:** Used when you want to create custom list styles or remove them entirely for navigation menus or other non-traditional lists.

<!-- end list -->

```css
img {
  max-width: 100%;
  height: auto;
  display: block; /* Removes extra space below images */
}
```

- `img`: Selects all image `<img>` elements.
- `max-width: 100%;`:
  - **Concept:** Ensures images are **responsive** and don't overflow their containers. The image will scale down if its parent container is smaller than its intrinsic width.
  - **In Detail:** This is a cornerstone of responsive web design. It ensures images never exceed the width of their containing element, preventing horizontal scrollbars on smaller screens.
- `height: auto;`:
  - **Concept:** When `max-width: 100%` is applied, `height: auto` maintains the image's **aspect ratio**.
  - **In Detail:** If you only set `width: 100%` without `height: auto`, the image might become distorted (stretched or squashed). `height: auto` tells the browser to calculate the height proportionally to the new width.
- `display: block;`:
  - **Concept:** Changes the display type of images from inline (default) to block.
  - **In Detail:** Inline elements can sometimes have extra space below them (due to `line-height` properties of text). Setting `display: block` removes this common spacing issue and also allows block-level properties like `margin-top`/`margin-bottom` to be applied directly.

<!-- end list -->

```css
h1,
h2,
h3,
h4,
h5,
h6 {
  line-height: 1.2;
}
```

- `h1, h2, h3, h4, h5, h6`: Selects all heading elements.
- `line-height: 1.2;`: Sets a slightly tighter line height for headings compared to body text.
  - **Concept:** Headings typically look better with less space between lines than paragraph text, which improves their visual impact.

---

### **Utility Classes (`/* --- Utility Classes --- */`)**

Reusable styles applied to elements using specific class names.

```css
.divider {
  width: 9.375rem; /* 150px */
  height: 0.25rem; /* 4px */
  background-color: #fc036b;
  margin: 1rem auto; /* Centered by default */
  border-radius: 5px;
}
```

- `.divider`: Selects any element with the class `divider`.
- `width: 9.375rem;` (150px): Fixed width for the divider.
- `height: 0.25rem;` (4px): Fixed height for the divider.
- `background-color: #fc036b;`: Sets the background color to a vibrant pink/red.
- `margin: 1rem auto;`:
  - **Concept:** This shorthand sets top/bottom margin to `1rem` and left/right margin to `auto`. For a block-level element with a defined width, `margin: auto` on left/right horizontally centers it within its parent.
- `border-radius: 5px;`: Adds slight rounded corners to the divider.

<!-- end list -->

```css
.button {
  display: inline-block;
  padding: 0.8rem 1.6rem;
  border-radius: 1.875rem; /* 30px */
  font-weight: 600;
  text-align: center;
  transition: background-color 0.3s ease, transform 0.2s ease;
}
```

- `.button`: Base styles for all buttons.
- `display: inline-block;`:
  - **Concept:** Allows an element to behave like an inline element (can sit next to other inline elements) but also accept block-level properties like `width`, `height`, and `padding`/`margin` on all sides.
  - **In Detail:** This is ideal for buttons, which need specific dimensions and padding but should also allow text to flow around them or sit in line with other elements.
- `padding: 0.8rem 1.6rem;`: Sets top/bottom padding to `0.8rem` and left/right padding to `1.6rem`.
- `border-radius: 1.875rem;` (30px): Creates very rounded, almost pill-shaped buttons.
- `font-weight: 600;`: Makes the button text semi-bold.
- `text-align: center;`: Centers the text inside the button.
- `transition: background-color 0.3s ease, transform 0.2s ease;`: Defines smooth transitions for animations.
  - **Concept:** When a property changes (e.g., on hover), instead of an abrupt change, the transition animates it over a specified duration and easing function.
  - **In Detail:**
    - `background-color 0.3s ease`: Animates background color changes over 0.3 seconds with an `ease` (slow start, fast middle, slow end) timing function.
    - `transform 0.2s ease`: Animates `transform` properties (like `translateY`) over 0.2 seconds.

<!-- end list -->

```css
.button--primary {
  background-color: #fc036b;
  color: #f5f5f5;
  border: 1px solid #fc036b;
}

.button--primary:hover {
  background-color: #e0025c; /* Slightly darker primary */
  transform: translateY(-2px);
}
```

- `.button--primary`: Specific styles for the primary button variation.
  - `background-color: #fc036b;`: Pink/red background.
  - `color: #f5f5f5;`: Light gray text.
  - `border: 1px solid #fc036b;`: A 1px solid border matching the background.
- `.button--primary:hover`: Styles applied when the mouse cursor hovers over the primary button.
  - `:hover`: A **pseudo-class** that selects an element when the user's pointing device is over it.
  - `background-color: #e0025c;`: Darkens the background slightly.
  - `transform: translateY(-2px);`: Moves the button slightly upwards by 2 pixels, creating a subtle "lift" effect.

<!-- end list -->

```css
.button--secondary {
  background-color: #484872;
  color: #f5f5f5;
  border: 1px solid #484872;
}

.button--secondary:hover {
  background-color: #3b3b5b; /* Slightly darker secondary */
  transform: translateY(-2px);
}
```

- `.button--secondary`: Styles for a secondary button variation (similar to primary but with a different color scheme).
  - Uses `#484872` (dark purple/blue) for background and border, and `#f5f5f5` for text.
  - Hover state darkens its background color as well.

---

### **Section Base Styling (`/* --- Section Base Styling --- */`)**

General styles applied to all main sections of the content.

```css
.section {
  padding: 4rem 2rem; /* 64px 32px */
  margin: 0 auto;
  max-width: 75rem; /* 1200px */
}
```

- `.section`: Selects any element with the class `section`.
- `padding: 4rem 2rem;`:
  - **Concept:** Provides inner spacing around the content of each section.
  - **In Detail:** `4rem` for top/bottom padding (64px based on 16px base font size) and `2rem` for left/right padding (32px). This creates breathing room around section content.
- `margin: 0 auto;`: Horizontally centers the section within its parent.
- `max-width: 75rem;` (1200px): Limits the maximum width of the section's content.
  - **Concept:** Prevents content from stretching too wide on large screens, which improves readability.
  - **In Detail:** Content is generally more readable when lines of text are not excessively long. This `max-width` ensures your main content blocks don't become unwieldy on very wide monitors.

<!-- end list -->

```css
.section__header {
  text-align: center;
  margin-bottom: 4rem; /* Standard space below section headers */
}

.section__title {
  font-size: 1.8rem; /* Mobile default */
  color: #484872;
}
```

- `.section__header`: Styles for a common header block within sections.
  - `text-align: center;`: Centers text within the header.
  - `margin-bottom: 4rem;`: Adds substantial space below the section header, separating it from the main content of the section.
- `.section__title`: Styles for the main title within a section.
  - `font-size: 1.8rem;`: Sets a default mobile font size for section titles. This will be overridden by media queries for larger screens.
  - `color: #484872;`: Sets the color of the section title.

---

### **Navbar (`/* --- Navbar --- */`)**

Styling for the website's top navigation bar.

```css
.navbar {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  color: #f5f5f5;
  z-index: 1000;
}
```

- `position: absolute;`:
  - **Concept:** Takes the element out of the normal document flow. Its position is relative to its nearest positioned ancestor (if any) or the initial containing block (the `<html>` element).
  - **In Detail:** Here, `top: 0;` and `left: 0;` place the navbar at the very top-left of the viewport. Since it's absolutely positioned, it won't push down the content that follows it (like the hero section).
- `top: 0; left: 0;`: Positions the element at the top-left corner.
- `width: 100%;`: Ensures it spans the full width of its containing block.
- `display: flex;`:
  - **Concept:** Initializes a **Flexbox** container. Flexbox is a one-dimensional layout system for distributing space among items in an interface.
  - **In Detail:** Extremely powerful for aligning items in a row or column.
- `justify-content: space-between;`:
  - **Concept:** Distributes space between flex items along the main axis.
  - **In Detail:** In a row (default flex-direction), this pushes the first item to the start, the last item to the end, and distributes remaining space evenly between them. Perfect for logo on left, menu on right.
- `align-items: center;`:
  - **Concept:** Aligns flex items along the cross axis (perpendicular to the main axis).
  - **In Detail:** In a row, this centers items vertically. Ensures logo and menu are vertically aligned.
- `padding: 1.5rem 2rem;`: Inner spacing for the navbar.
- `color: #f5f5f5;`: Sets default text color for navbar elements (like logo).
- `z-index: 1000;`:
  - **Concept:** Controls the stacking order of positioned elements. Elements with a higher `z-index` appear on top of elements with a lower `z-index`.
  - **In Detail:** A high `z-index` ensures the navbar always stays on top of other content, even when scrolling.

<!-- end list -->

```css
.navbar__logo {
  font-size: 1.8rem;
  font-weight: 700;
  color: #f5f5f5;
  z-index: 1001; /* Ensure logo is above mobile menu when open */
}
```

- `.navbar__logo`: Styles the logo text.
- `font-size`, `font-weight`, `color`: Standard text styling.
- `z-index: 1001;`: Slightly higher `z-index` than the `navbar` itself, ensuring the logo is visible even if the mobile menu (`navbar__nav-list`) opens over it.

<!-- end list -->

```css
.navbar__nav-list {
  display: flex;
  flex-direction: column; /* Mobile default */
  position: fixed;
  top: 0;
  right: 0;
  width: 70%;
  max-width: 18.75rem; /* 300px */
  height: 100vh;
  background-color: #484872;
  transform: translateX(100%); /* Hidden by default */
  transition: transform 0.3s ease-in-out;
  padding-top: 5rem;
  box-shadow: -2px 0 10px rgba(0, 0, 0, 0.2);
  z-index: 999; /* Adjusted z-index to be below menu button */
}
```

- `.navbar__nav-list`: Styles the navigation menu, specifically designed for mobile first (off-screen).
- `display: flex; flex-direction: column;`: Makes the menu items stack vertically.
- `position: fixed;`:
  - **Concept:** Positions the element relative to the **viewport**. It stays in the same place even if the page scrolls.
  - **In Detail:** Used here to create a fixed sidebar menu that slides in from the right.
- `top: 0; right: 0;`: Anchors the menu to the top-right corner of the viewport.
- `width: 70%; max-width: 18.75rem;`: Sets the width of the menu to 70% of the viewport, but no wider than 300px.
- `height: 100vh;`: Makes the menu span the full height of the viewport. (`vh` = viewport height).
- `background-color: #484872;`: Dark background for the menu.
- `transform: translateX(100%);`:
  - **Concept:** Applies a 2D translation (movement) along the X-axis. `100%` means move it by 100% of its own width.
  - **In Detail:** This initially moves the entire menu off-screen to the right, effectively hiding it.
- `transition: transform 0.3s ease-in-out;`: Animates the `transform` property over 0.3 seconds. When `transform` changes (e.g., to `translateX(0)`), it will slide smoothly.
- `padding-top: 5rem;`: Adds space at the top for the menu content.
- `box-shadow: -2px 0 10px rgba(0, 0, 0, 0.2);`: Adds a shadow on the left side of the menu when it's open, giving it depth.
- `z-index: 999;`: A `z-index` of 999 places it below the logo and menu button (`z-index: 1001`) but above most other content.

<!-- end list -->

```css
.navbar__nav-list--active {
  transform: translateX(0); /* Slide in */
}
```

- `.navbar__nav-list--active`: This class is _added by JavaScript_ when the menu button is clicked.
- `transform: translateX(0);`: Moves the menu back to its original position (0% translation), making it slide into view.

<!-- end list -->

```css
.navbar__nav-item {
  margin-bottom: 1.5rem;
  text-align: center;
}

.navbar__nav-link {
  font-size: 1.125rem;
  padding: 0.5rem 1rem;
  display: block;
  transition: color 0.3s ease, background-color 0.3s ease;
}

.navbar__nav-link:hover,
.navbar__nav-link--active {
  color: #fc036b;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 5px;
}

.navbar__nav-item--cta {
  margin-top: 2rem;
}
```

- `navbar__nav-item`: Styles individual list items in the nav menu.
  - `margin-bottom: 1.5rem;`: Vertical spacing between menu items.
  - `text-align: center;`: Centers the link text.
- `navbar__nav-link`: Styles the actual links within the menu.
  - `font-size: 1.125rem;`: Larger font for mobile links.
  - `padding: 0.5rem 1rem;`: Padding around the link text, making it easier to tap.
  - `display: block;`: Makes the entire padding area clickable.
  - `transition: color 0.3s ease, background-color 0.3s ease;`: Smooth transition for hover effects.
- `navbar__nav-link:hover, .navbar__nav-link--active`: Styles applied on hover or when a link is actively selected.
  - `color: #fc036b;`: Changes text color to pink.
  - `background-color: rgba(255, 255, 255, 0.1);`: Adds a subtle, slightly transparent white background.
  - `border-radius: 5px;`: Rounds the corners of the background.
- `navbar__nav-item--cta`: Specific top margin for the CTA button in the nav list.

<!-- end list -->

```css
.navbar__menu-button {
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
  display: block; /* Show on mobile */
  z-index: 1001; /* Ensure menu button is above nav list */
}

.navbar__menu-button img {
  width: 2.5rem; /* 40px */
  height: 2.5rem;
}
```

- `navbar__menu-button`: Styles the hamburger menu button.
  - `background: none; border: none;`: Removes default button styles.
  - `cursor: pointer;`: Changes cursor to a hand on hover, indicating it's clickable.
  - `padding: 0.5rem;`: Padding around the icon for easier clicking.
  - `display: block;`: Ensures it's visible.
  - `z-index: 1001;`: Ensures it's always on top.
- `navbar__menu-button img`: Styles the image inside the button.
  - `width: 2.5rem; height: 2.5rem;`: Fixed size for the menu icon.

---

### **Hero Header (`/* --- Hero Header --- */`)**

Styling for the main introductory section of the page.

```css
.hero-header {
  width: 100%;
  min-height: 100vh;
  background: url(./images/header-bg.png) no-repeat center center/cover;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  text-align: center;
  color: #f5f5f5;
  padding-bottom: 4rem;
  position: relative;
}
```

- `hero-header`: Selects the hero section.
- `width: 100%;`: Full width.
- `min-height: 100vh;`: Ensures the hero section takes up at least the full height of the viewport.
- `background: url(./images/header-bg.png) no-repeat center center/cover;`: Sets a background image.
  - **Concept:** Shorthand for `background-image`, `background-repeat`, `background-position`, and `background-size`.
  - **In Detail:**
    - `url(...)`: Specifies the image.
    - `no-repeat`: Prevents the image from tiling.
    - `center center`: Centers the image horizontally and vertically.
    - `/cover`: **Scales the image** to cover the entire container, even if it has to crop parts of the image. Ensures no empty space.
- `display: flex; flex-direction: column;`: Makes the content inside stack vertically.
- `justify-content: flex-end;`: Aligns content to the bottom of the flex container (the hero section).
- `align-items: center;`: Centers content horizontally along the cross-axis.
- `text-align: center;`: Centers text within the hero content.
- `color: #f5f5f5;`: White/light text color for contrast against the background image.
- `padding-bottom: 4rem;`: Adds space at the bottom, lifting content slightly from the very edge.
- `position: relative;`: Important because the `navbar` is `position: absolute;`. A `position: relative` parent makes `position: absolute` children positioned relative to it.

<!-- end list -->

```css
.hero-header__content {
  margin-bottom: 4rem;
  padding: 0 1.5rem;
  max-width: 75rem;
  width: 100%;
}

.hero-header__subtitle {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
}

.hero-header__title {
  font-size: 2.5rem;
  margin-top: 2rem;
  margin-bottom: 2rem;
}
```

- `hero-header__content`: Container for the main text in the hero.
  - `margin-bottom: 4rem;`: Space below the content.
  - `padding: 0 1.5rem;`: Horizontal padding.
  - `max-width: 75rem; width: 100%;`: Constrains content width while ensuring it uses full width on smaller screens.
- `hero-header__subtitle`, `hero-header__title`: Specific font sizes and margins for the hero's headings.

---

### **Events Section (`/* --- Events Section --- */`)**

```css
.events-section__grid {
  display: grid;
  grid-template-columns: 1fr; /* Single column for mobile */
  gap: 3rem;
  justify-items: center;
  align-items: start;
}
```

- `events-section__grid`: Sets up a **CSS Grid** container.
  - **Concept:** CSS Grid is a two-dimensional layout system (rows and columns) that is highly effective for complex layouts.
- `display: grid;`: Initializes the grid container.
- `grid-template-columns: 1fr;`: For mobile, creates a single column that takes up all available space.
  - **Concept:** `1fr` means "1 fraction of the available space."
- `gap: 3rem;`: Sets the spacing between grid items (both rows and columns).
- `justify-items: center;`: Horizontally centers grid items within their grid cells.
- `align-items: start;`: Vertically aligns grid items to the start of their grid cells.

<!-- end list -->

```css
.event-card {
  text-align: center;
  background-color: #fff;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  padding-bottom: 2rem;
  max-width: 25rem; /* Limit card width on mobile for better readability */
}

.event-card__image {
  width: 100%;
  height: 12.5rem; /* 200px */
  object-fit: cover;
  margin-bottom: 2rem;
}

.event-card__title {
  font-size: 1.5rem;
  color: #484872;
  margin-bottom: 0.625rem;
  padding: 0 2rem;
}

.event-card__description {
  color: #7c7c7c;
  font-size: 0.9375rem;
  margin-bottom: 2rem;
  padding: 0 2rem;
}
```

- `event-card`: Styles individual event cards.
  - `text-align: center;`: Centers text inside the card.
  - `background-color: #fff;`: White background.
  - `border-radius: 5px;`: Slightly rounded corners.
  - `overflow: hidden;`: Hides any content that goes outside the border-radius (important for image at top).
  - `box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);`: Adds a subtle shadow for a lifted effect. `rgba` allows for transparency (`0.1` is 10% opacity).
  - `padding-bottom: 2rem;`: Padding at the bottom of the card.
  - `max-width: 25rem;`: Limits the card's width on mobile to prevent it from getting too wide.
- `event-card__image`: Image specific styles.
  - `width: 100%; height: 12.5rem;`: Makes image full width of card and fixed height.
  - `object-fit: cover;`: **Scales the image** to fill the content box while maintaining its aspect ratio. It will crop parts of the image if necessary. This is crucial for consistent image sizes in cards.
- `event-card__title`, `event-card__description`: Specific styling for text within cards (font size, color, margins, padding).

---

### **Explore Section (`/* --- Explore Section --- */`)**

```css
.explore-section {
  background: url("./images/bg2.png") no-repeat center center/cover;
  min-height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #f5f5f5;
  text-align: center;
}

.explore-section__content {
  padding: 2rem;
  background-color: rgba(0, 0, 0, 0.5); /* Semi-transparent overlay */
  border-radius: 5px;
  max-width: 37.5rem; /* 600px */
}

.explore-section__title {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: inherit; /* Inherit from parent */
}

.explore-section__description {
  margin-top: 2rem;
  margin-bottom: 4rem;
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.9);
}
```

- `explore-section`: A full-width section with a background image.
  - Similar background properties to `hero-header`.
  - `min-height: 80vh;`: Ensures it's at least 80% of viewport height.
  - `display: flex; align-items: center; justify-content: center;`: Uses Flexbox to perfectly center its _single_ child (`explore-section__content`) both horizontally and vertically.
- `explore-section__content`: The content box within the `explore-section`.
  - `background-color: rgba(0, 0, 0, 0.5);`: Creates a semi-transparent black overlay, making text readable over the background image.
- `explore-section__title`, `explore-section__description`: Styling for text within this section.
  - `color: inherit;`: Title inherits the `color: #f5f5f5;` from `explore-section`.

---

### **Tours Section (`/* --- Tours Section --- */`)**

```css
.tours-section {
  display: flex;
  flex-direction: column; /* Mobile default */
  gap: 3rem;
  align-items: center;
}

.tours-section__content {
  text-align: center; /* Center text on mobile */
}

.tours-section__title {
  font-size: 1.8rem;
  color: #484872;
  margin-bottom: 1rem;
}

.tours-section__content .divider {
  margin-left: auto;
  margin-right: auto;
}

.tours-section__description {
  margin: 2rem 0;
  color: #7c7c7c;
}

.tours-section__gallery {
  display: grid;
  /* Using auto-fit with minmax to create flexible columns */
  grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
  gap: 0.75rem;
  width: 100%;
}

.tours-section__gallery img {
  width: 100%;
  aspect-ratio: 4/3; /* Maintain 4:3 aspect ratio */
  max-height: 350px;
  object-fit: cover;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}
```

- `tours-section`: Main container for tours content.
  - `flex-direction: column;`: Stacks content vertically on mobile.
- `tours-section__content`: Text content beside the gallery.
- `tours-section__gallery`: The image gallery using CSS Grid.
  - `grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));`: **This is a powerful responsive grid technique.**
    - `repeat()`: Creates repeated columns.
    - `auto-fit`: Creates as many columns as can fit into the container.
    - `minmax(16rem, 1fr)`: Each column will be at least `16rem` (256px) wide. If there's extra space, it will be distributed evenly (`1fr`) among the columns. If `16rem` is too wide for available space, columns will wrap. This makes the grid very flexible.
  - `gap: 0.75rem;`: Spacing between gallery images.
- `tours-section__gallery img`: Styles individual images in the gallery.
  - `aspect-ratio: 4/3;`: **Modern CSS property** to maintain a specific width-to-height ratio for an element. This ensures all your gallery images have the same proportion, even if their original dimensions vary, preventing layout shifts and making the grid look uniform.
  - `max-height: 350px;`: Prevents images from becoming excessively tall on very wide screens.
  - `object-fit: cover;`: Crops images to fit the `aspect-ratio` without distortion.

---

### **About Section (`/* --- About Section --- */`)**

```css
.about-section {
  display: flex;
  flex-direction: column; /* Stack on mobile */
  align-items: center;
  gap: 3rem;
  text-align: center; /* Center text on mobile */
}

.about-section__content {
  max-width: 40rem;
}

.about-section__title {
  margin-bottom: 1rem;
  font-size: 1.8rem;
}

.about-section__description {
  color: #555;
  margin-bottom: 1rem;
}

.about-section__description:last-of-type {
  margin-bottom: 2rem;
}

.about-section__image-container {
  width: 100%;
  max-width: 30rem;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}

.about-section__image {
  width: 100%;
  height: 18.75rem; /* 300px default height */
  object-fit: cover;
}
```

- `about-section`: Another Flexbox container, stacking content and image vertically on mobile.
- `about-section__content`: Text content of the about section.
- `about-section__description:last-of-type`:
  - **Concept:** A **pseudo-class** that selects an element that is the last sibling of its type.
  - **In Detail:** Here, it ensures the last paragraph has more margin below it, creating space before the button.
- `about-section__image-container`: A container for the about image, providing styling like `border-radius` and `box-shadow`.
- `about-section__image`: The image itself, with `object-fit: cover` to maintain aspect ratio within the fixed `height`.

---

### **Contact Section (`/* --- Contact Section --- */`)**

```css
.contact-section__intro {
  text-align: center;
  margin-bottom: 2rem;
  color: #555;
  max-width: 40rem;
  margin-left: auto;
  margin-right: auto;
}

.contact-form {
  max-width: 40rem;
  margin: 0 auto;
  padding: 2rem;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-size: 0.95rem;
  font-weight: 600;
  color: #484872;
  margin-bottom: 0.5rem;
}

.form-group input[type="text"],
.form-group input[type="email"],
.form-group textarea {
  padding: 0.8rem 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-family: "Poppins", sans-serif;
  font-size: 1rem;
  color: #333;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.form-group input[type="text"]:focus,
.form-group input[type="email"]:focus,
.form-group textarea:focus {
  border-color: #fc036b;
  box-shadow: 0 0 0 3px rgba(252, 3, 107, 0.2); /* Pink glow on focus */
  outline: none; /* Remove default outline */
}

.form-group textarea {
  resize: vertical; /* Allow vertical resizing only */
  min-height: 6rem;
}

.contact-form .button--primary {
  width: fit-content;
  align-self: center;
  margin-top: 1rem;
}
```

- `contact-section__intro`: Introductory text for the contact form, centered and limited in width.
- `contact-form`: Styles the form container.
  - `display: flex; flex-direction: column; gap: 1.5rem;`: Uses Flexbox to stack form groups vertically with consistent spacing.
  - `background-color: #f9f9f9;`: Light gray background for the form.
- `form-group`: Styles a container for a label and its input.
  - `display: flex; flex-direction: column;`: Stacks label and input vertically.
- `form-group label`: Styles the form labels.
- `form-group input[type="text"], ... textarea`: Selects specific input types and text areas.
  - `padding`, `border`, `border-radius`, `font-family`, `font-size`, `color`: Standard input styling.
  - `transition: border-color 0.3s ease, box-shadow 0.3s ease;`: Smooth transition for focus effects.
- `form-group input[type="text"]:focus, ... textarea:focus`: Styles applied when an input field is focused (clicked into).
  - `:focus`: A **pseudo-class** that selects an element when it has received focus (e.g., via keyboard tabbing or clicking).
  - `border-color: #fc036b;`: Changes border color to pink.
  - `box-shadow: 0 0 0 3px rgba(252, 3, 107, 0.2);`: Adds a pink "glow" effect.
  - `outline: none;`: Removes the browser's default blue/black outline on focus, allowing your custom `box-shadow` to be the primary focus indicator. (Good for design, but ensure the `box-shadow` is strong enough for accessibility).
- `form-group textarea`: Specific styles for the textarea.
  - `resize: vertical;`: Allows the user to only resize the textarea vertically, not horizontally (which can break layout).
  - `min-height: 6rem;`: Minimum height for the textarea.
- `contact-form .button--primary`: Styles the submit button within the form.
  - `width: fit-content;`: The button's width will shrink to fit its content.
  - `align-self: center;`: Centers the button horizontally within the flex container (`contact-form`).

---

### **Footer (`/* --- Footer --- */`)**

```css
.footer {
  background-color: #484872;
  color: #f5f5f5;
  text-align: center;
  padding: 2rem;
  font-size: 0.875rem; /* 14px */
}

.footer__text {
  margin: 0.5rem 0;
  opacity: 0.9;
}
```

- `footer`: Styles the site-wide footer.
  - `background-color: #484872;`: Dark background.
  - `color: #f5f5f5;`: Light text.
  - `padding: 2rem;`: Inner spacing.
  - `font-size: 0.875rem;`: Slightly smaller font size for footer text.
- `footer__text`: Styles individual paragraphs within the footer.
  - `margin: 0.5rem 0;`: Vertical spacing between footer text lines.
  - `opacity: 0.9;`: Makes the text slightly transparent.

---

### **Media Queries (`/* --- Media Queries --- */`)**

These are the core of **Responsive Web Design**. They allow you to apply different CSS rules based on various characteristics of the device, most commonly screen width.

```css
/* Tablet breakpoint - min-width 768px */
@media (min-width: 768px) {
  /* ... CSS rules for screens 768px wide and up ... */
}

/* Desktop breakpoint - min-width 1024px */
@media (min-width: 1024px) {
  /* ... CSS rules for screens 1024px wide and up ... */
}
```

- `@media (min-width: 768px)`:

  - **Concept:** This is a **media query**. The CSS rules inside these curly braces will _only apply_ when the viewport (the visible area of the browser window) is at least `768px` wide.
  - **In Detail:** This is a "mobile-first" approach. You style for the smallest screens first (outside any media query), then progressively enhance the layout and styles for larger screens. This generally leads to more performant and robust responsive designs.

- `min-width`: The rules apply when the viewport width is _greater than or equal to_ the specified value.

- Inside each media query, you're overriding or adding styles for specific elements:

  - **Navbar:** Changes `flex-direction` to `row` for horizontal layout, removes `position: fixed` and related mobile-specific styles, and hides the menu button.
  - **Hero Header:** Increases font sizes for title and subtitle for larger screens.
  - **Section Titles:** Increases default font size from `1.8rem` to `2.5rem` for sections.
  - **Events Section Grid:** Changes `grid-template-columns` to `repeat(auto-fit, minmax(280px, 1fr))` for tablet, allowing multiple columns.
  - **About Section:** Changes `flex-direction` to `row` to place content and image side-by-side, adjusts text alignment and image container width.
  - **Explore Section:** Increases max-width and font size for the content block.
  - **Tours Section:** Changes `flex-direction` to `row` for side-by-side layout, adjusts `padding-right` for content, centers `divider` to the left, and adjusts `grid-template-columns` for the gallery. The `minmax(10rem, 1fr)` ensures flexible columns that are at least 10rem wide.

- The Desktop breakpoint (`min-width: 1024px`) further refines these styles for even larger screens, often making elements even bigger or adjusting column counts (e.g., `events-section__grid` goes to `repeat(2, 1fr)` which makes two even columns, `tours-section__gallery` again uses `repeat(2, 1fr)` for its side-by-side grid of images, and about section elements adjust `flex-basis` and `height`).

---

### **Key CSS Concepts Applied in Your Code:**

- **Box Model:** Understanding `margin`, `padding`, `border`, `content-box`, and `border-box`.
- **Selectors:** Universal (`*`), type (`body`, `a`, `img`), class (`.button`, `.navbar`), pseudo-elements (`::before`, `::after`), pseudo-classes (`:hover`, `:focus`, `:last-of-type`), attribute (`[type="text"]`).
- **Units:** `rem` for scalable sizes, `px` for fixed sizes, `%` for relative sizes, `vh` for viewport relative height.
- **Layout:**
  - **Flexbox (`display: flex`)**: For one-dimensional alignment and distribution (e.g., navbar, stacking items, centering content).
  - **CSS Grid (`display: grid`)**: For two-dimensional, more complex layouts (e.g., event cards, image galleries). `auto-fit` with `minmax` is excellent for responsive grids.
- **Positioning:** `static` (default), `relative`, `absolute`, `fixed`. `z-index` for stacking.
- **Typography:** `font-family`, `font-size`, `line-height`, `font-weight`, `text-align`.
- **Visual Properties:** `background`, `color`, `border`, `border-radius`, `box-shadow`, `opacity`, `overflow`.
- **Transitions:** For smooth animations on state changes (`:hover`, `:focus`).
- **Responsive Design:** `max-width` on images and sections, `media queries` to adapt styles to different screen sizes, "mobile-first" approach.

Your CSS is well-structured, follows modern practices (like `rem` units, `box-sizing: border-box`, Flexbox, and Grid), and demonstrates a strong understanding of responsive design. Excellent work!
