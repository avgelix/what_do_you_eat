# Data Directory

Place cleaned datasets here.

## Current Data

- `products.json` - Main dataset (2,000+ products from 5 countries)
- `categories.json` - Food category metadata

## Data Format

JSON is used for easy client-side loading and manipulation.

## Usage

Data is loaded asynchronously via JavaScript:

```javascript
const response = await fetch('/data/products.json');
const data = await response.json();
```

## Data Integrity

**DO NOT modify source data files directly.** 

For filtering or transformations, work with copies in memory. Keep the original data pristine for reproducibility.

## Attribution

All data sourced from [Open Food Facts](https://world.openfoodfacts.org/) under ODbL license.
