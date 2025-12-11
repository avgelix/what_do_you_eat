# Fonts Directory

Place self-hosted web fonts here.

## Recommended Format

- **WOFF2**: Modern format, best compression (primary)
- **WOFF**: Fallback for older browsers

## Font Loading Strategy

Use `font-display: swap` in @font-face declarations to prevent invisible text during loading.

## Example

```css
@font-face {
  font-family: 'Publico';
  src: url('../assets/fonts/publico-bold.woff2') format('woff2'),
       url('../assets/fonts/publico-bold.woff') format('woff');
  font-weight: 700;
  font-style: normal;
  font-display: swap;
}
```

## Current Fallbacks

The site currently uses system fonts as fallbacks:
- **Headings**: Georgia, Times (serif)
- **UI Elements**: Helvetica Neue, Arial (sans-serif)

Add custom fonts here when ready.
