# Comprehensive Tailwind CSS Cheatsheet

## Layout

### Container
- `container`: Set the max-width to match the min-width of the current breakpoint

### Display
- `block`: `display: block;`
- `inline-block`: `display: inline-block;`
- `inline`: `display: inline;`
- `flex`: `display: flex;`
- `inline-flex`: `display: inline-flex;`
- `grid`: `display: grid;`
- `hidden`: `display: none;`

### Flexbox
- `flex-row`: `flex-direction: row;`
- `flex-col`: `flex-direction: column;`
- `flex-wrap`: `flex-wrap: wrap;`
- `flex-nowrap`: `flex-wrap: nowrap;`
- `items-start`: `align-items: flex-start;`
- `items-center`: `align-items: center;`
- `items-end`: `align-items: flex-end;`
- `justify-start`: `justify-content: flex-start;`
- `justify-center`: `justify-content: center;`
- `justify-end`: `justify-content: flex-end;`
- `justify-between`: `justify-content: space-between;`

### Grid
- `grid-cols-{n}`: `grid-template-columns: repeat(n, minmax(0, 1fr));`
- `col-span-{n}`: `grid-column: span n / span n;`
- `gap-{size}`: `gap: {size};`

### Positioning
- `static`: `position: static;`
- `fixed`: `position: fixed;`
- `absolute`: `position: absolute;`
- `relative`: `position: relative;`
- `sticky`: `position: sticky;`

## Spacing

### Padding
- `p-{size}`: padding on all sides
- `px-{size}`: padding on left and right
- `py-{size}`: padding on top and bottom
- `pt-{size}`, `pr-{size}`, `pb-{size}`, `pl-{size}`: padding on specific sides

### Margin
- `m-{size}`: margin on all sides
- `mx-{size}`: margin on left and right
- `my-{size}`: margin on top and bottom
- `mt-{size}`, `mr-{size}`, `mb-{size}`, `ml-{size}`: margin on specific sides

## Sizing

### Width
- `w-{size}`: width
- `w-full`: width: 100%;
- `w-screen`: width: 100vw;

### Height
- `h-{size}`: height
- `h-full`: height: 100%;
- `h-screen`: height: 100vh;

## Typography

### Font Family
- `font-sans`: Sans-serif font stack
- `font-serif`: Serif font stack
- `font-mono`: Monospace font stack

### Font Size
- `text-xs`, `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, etc.

### Font Weight
- `font-thin`, `font-light`, `font-normal`, `font-medium`, `font-bold`, `font-extrabold`

### Text Alignment
- `text-left`, `text-center`, `text-right`, `text-justify`

### Text Color
- `text-{color}-{shade}`: e.g., `text-blue-500`, `text-red-700`

## Backgrounds

### Background Color
- `bg-{color}-{shade}`: e.g., `bg-blue-500`, `bg-red-700`

### Background Size
- `bg-auto`, `bg-cover`, `bg-contain`

## Borders

### Border Width
- `border`, `border-0`, `border-2`, `border-4`, `border-8`

### Border Color
- `border-{color}-{shade}`: e.g., `border-blue-500`, `border-red-700`

### Border Radius
- `rounded`, `rounded-sm`, `rounded-md`, `rounded-lg`, `rounded-full`

## Effects

### Opacity
- `opacity-{percentage}`: e.g., `opacity-50`, `opacity-75`

### Box Shadow
- `shadow`, `shadow-sm`, `shadow-md`, `shadow-lg`, `shadow-xl`, `shadow-2xl`

## Interactivity

### Cursor
- `cursor-pointer`, `cursor-not-allowed`

### User Select
- `select-none`, `select-text`, `select-all`, `select-auto`

## Responsive Design

### Breakpoints
- `sm:`: min-width: 640px
- `md:`: min-width: 768px
- `lg:`: min-width: 1024px
- `xl:`: min-width: 1280px
- `2xl:`: min-width: 1536px

Usage: `md:text-lg` applies `text-lg` at medium screens and above

## Pseudo-classes

### Hover
- `hover:{utility}`: e.g., `hover:bg-blue-700`

### Focus
- `focus:{utility}`: e.g., `focus:outline-none`

### Active
- `active:{utility}`: e.g., `active:bg-blue-800`

## Customization

### Extending Theme
```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        'custom-blue': '#1da1f2',
      },
      spacing: {
        '72': '18rem',
        '84': '21rem',
      },
    }
  }
}
```

### Creating Utilities
```javascript
// tailwind.config.js
module.exports = {
  theme: {
    // ...
  },
  plugins: [
    function({ addUtilities }) {
      const newUtilities = {
        '.rotate-45': {
          transform: 'rotate(45deg)',
        },
        '.rotate-90': {
          transform: 'rotate(90deg)',
        },
      }
      addUtilities(newUtilities)
    }
  ]
}
```

This cheat sheet covers the most commonly used utilities and concepts in Tailwind CSS. Remember that Tailwind is highly customizable, so you can extend or modify these utilities to fit your project's needs.
