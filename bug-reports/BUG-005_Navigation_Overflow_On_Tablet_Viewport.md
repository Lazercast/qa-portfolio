# BUG-005 — Navigation Menu Items Overflow and Overlap on Tablet Viewport (768px)

---

## Summary

On tablet-sized viewports (768px–1024px width), the primary navigation menu items overflow their container and overlap with the site logo and the search bar. The navigation is unusable at this screen size, as overlapping elements obscure both the menu links and the search functionality.

---

## Bug Details

| Field            | Details                          |
|------------------|----------------------------------|
| **Bug ID**       | BUG-005                          |
| **Title**        | Navigation menu items overflow and overlap on tablet viewport (768px–1024px) |
| **Type**         | UI / Mobile Responsiveness       |
| **Severity**     | Medium                           |
| **Priority**     | Medium                           |
| **Status**       | Open                             |
| **Reported By**  | QA Engineer                      |
| **Date Reported**| 2025-06-03                       |
| **Assigned To**  | Frontend / CSS Team              |

---

## Environment

| Parameter        | Value                            |
|------------------|----------------------------------|
| **Application**  | ShopEasy E-Commerce (demo)       |
| **URL**          | `https://demo.shopeasy.io` (all pages) |
| **Browser**      | Chrome 124.0, Safari 17.4       |
| **OS**           | Windows 11 / iPadOS 17.4        |
| **Device**       | iPad Air (5th gen), Browser DevTools responsive mode |
| **Viewport**     | 768px × 1024px, 900px × 1200px  |
| **Network**      | Wi-Fi                            |

---

## Preconditions

- Any page on the application is open (the bug affects the global navigation component).
- The browser window is resized to a width between **768px and 1024px**, or a physical tablet device is used.
- No browser zoom is applied (100% zoom).

---

## Steps to Reproduce

1. Open `https://demo.shopeasy.io` in Chrome.
2. Open **DevTools** (F12) and activate **Responsive Design Mode** (Ctrl+Shift+M).
3. Set the viewport width to **768px** (height can be any value).
4. Observe the top navigation bar.
5. Repeat at viewport widths of **800px**, **900px**, and **1024px**.

---

## Expected Result

At tablet-sized viewports (768px–1024px), the navigation should respond gracefully. Acceptable behaviours include:

- A **hamburger menu** (collapsible menu icon) that expands on tap/click.
- Navigation items that **wrap to a second line** within the header.
- A **condensed horizontal menu** with shorter labels or icons.

In all cases, no elements should overlap and all navigation links and the search bar should remain fully accessible.

---

## Actual Result

At **768px viewport width**:

- All 7 navigation menu items (`Home`, `Shop`, `Categories`, `Deals`, `Wishlist`, `Account`, `Contact`) attempt to render in a single horizontal row.
- The items overflow the header container and extend over the **site logo** on the left and the **search bar** on the right.
- The logo is partially hidden behind the menu text.
- The search bar input field is completely obscured.
- Clicking affected areas produces unpredictable results (the click lands on the overlapping nav item rather than the logo or search bar).

The issue begins at **1010px** and worsens as the viewport narrows toward **768px**.

---

## Visual Evidence Description

At 768px width, the nav bar shows all menu items compressed into a single row exceeding the available width by approximately 240px, with items rendering beyond the right edge of the viewport and overlapping interactive elements.

---

## Additional Information

- The navigation renders correctly on:
  - **Desktop (≥1280px):** All items visible and properly spaced.
  - **Mobile (≤480px):** A hamburger menu correctly replaces the nav bar.
- The **breakpoint gap** between 481px and 1024px has no responsive CSS rule applied — this appears to be the root cause.
- Inspecting the CSS in DevTools shows the `.nav-menu` element has `display: flex` and `flex-wrap: nowrap` with no `@media` rule targeting this range.

---

## Attachments

- `screenshot_nav_desktop_1280px.png` — Correct navigation at desktop width
- `screenshot_nav_tablet_768px.png` — Overflow and overlap issue at 768px
- `screenshot_nav_mobile_375px.png` — Correct hamburger menu at mobile width
- `css_nav_snippet.txt` — Extracted CSS for `.nav-menu` component

---

## Suggested Fix

Add a CSS media query targeting the **tablet breakpoint** (481px–1024px). The simplest fix is to change `flex-wrap: nowrap` to `flex-wrap: wrap` within this range, or to apply the existing mobile hamburger menu pattern to the tablet range as well. Coordinate with the designer for the preferred tablet navigation pattern.

```css
/* Suggested fix — tablet breakpoint */
@media (min-width: 481px) and (max-width: 1024px) {
  .nav-menu {
    display: none; /* Switch to hamburger menu */
  }
  .nav-hamburger {
    display: flex;
  }
}
```
