# Guide: Finding and Editing Banner Image Positions

## Quick Reference: Key CSS Locations

### 1. **Desktop Banner Starting Position** (Initial Load)
**File:** `styles.css`  
**Line:** ~209-214  
**Selector:** `.banner-wrap` inside `@media (min-width: 1024px)`

```css
@media (min-width: 1024px) {
  .banner-wrap {
    margin-top: 120px; /* ← THIS controls how far down the banner starts */
    top: 0 !important;
    position: sticky;
  }
}
```

**What to change:** Increase `margin-top: 120px` to a larger value (e.g., `150px`, `180px`) to push the banner further down.

---

### 2. **Banner Background Image** (`Banner_bg_only.png`)
**File:** `styles.css`  
**Line:** ~216-221  
**Selector:** `.banner-image` inside `@media (min-width: 1024px)`

```css
.banner-image {
  margin-top: 0;
  object-position: center top; /* ← Controls which part of image is visible */
  max-height: 140px;
  min-height: 100px;
}
```

**What to change:**
- `margin-top`: Add spacing above the image itself
- `object-position`: Change from `center top` to `center center` or `center bottom` to show different parts of the image

---

### 3. **Banner Title Image** (`DwD_title.png`)
**File:** `styles.css`  
**Line:** ~223-227  
**Selector:** `.banner-title` inside `@media (min-width: 1024px)`

```css
.banner-title {
  max-width: 35%;
  top: 70%; /* ← Vertical position within banner (70% from top) */
  transition: opacity 0.3s ease, transform 0.3s ease;
}
```

**What to change:**
- `top: 70%`: Increase to `75%` or `80%` to move title down within the banner
- `max-width: 35%`: Adjust size if needed

---

### 4. **Navbar Height** (Reference)
**File:** `styles.css`  
**Line:** ~1383-1384  
**Selector:** `.navbar` inside `@media (min-width: 1024px)`

```css
.navbar {
  height: 72px; /* ← Current navbar height */
}
```

**Why this matters:** The banner's `margin-top` should be at least equal to or greater than this value to start below the navbar.

---

## How to Find These in Your Code

### Method 1: Search in Your Editor
1. Open `styles.css`
2. Press `Ctrl+F` (or `Cmd+F` on Mac)
3. Search for:
   - `banner-wrap` - Finds the main container
   - `banner-image` - Finds the background image styles
   - `banner-title` - Finds the title image styles
   - `@media (min-width: 1024px)` - Finds desktop-specific styles

### Method 2: Use Browser Dev Tools
1. **Open your page in a browser**
2. **Right-click on the banner** → "Inspect" or "Inspect Element"
3. **In the Elements panel**, you'll see:
   - `.banner-wrap` - The container
   - `.banner-image` - The background image
   - `.banner-title` - The title image
4. **In the Styles panel**, you can:
   - See all CSS rules affecting the element
   - See which rules are active (highlighted)
   - See computed values (actual pixel positions)
   - Temporarily edit values to test

### Method 3: Check Computed Values
1. In Dev Tools, select `.banner-wrap`
2. Look at the **Computed** tab
3. Find:
   - `margin-top` - Shows actual spacing from top
   - `top` - Shows sticky position
   - `height` - Shows actual height

---

## Step-by-Step: Adjusting Banner Position

### To Move Banner Further Down:
1. Open `styles.css`
2. Go to line ~210
3. Find: `margin-top: 120px;`
4. Change to: `margin-top: 150px;` (or higher)
5. Save and refresh

### To Adjust Title Position Within Banner:
1. Open `styles.css`
2. Go to line ~225
3. Find: `top: 70%;`
4. Change to: `top: 75%;` (moves down) or `top: 65%;` (moves up)
5. Save and refresh

### To Show Different Part of Background Image:
1. Open `styles.css`
2. Go to line ~218
3. Find: `object-position: center top;`
4. Change to: `object-position: center center;` or `center bottom;`
5. Save and refresh

---

## Important Notes

- **Desktop only:** These changes are inside `@media (min-width: 1024px)`, so they only affect desktop screens
- **Mobile separate:** Mobile styles are in `@media (max-width: 1023px)` or `@media (max-width: 767px)`
- **Use `!important` carefully:** Some rules use `!important` which overrides other styles
- **Test after changes:** Always refresh your browser to see changes

---

## Current Values Summary

- **Navbar height:** `72px`
- **Banner margin-top (desktop):** `120px`
- **Banner image max-height:** `140px`
- **Banner title top position:** `70%`
- **Banner title max-width:** `35%`
