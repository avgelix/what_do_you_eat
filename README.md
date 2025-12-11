# What Do You Eat

A data storytelling website exploring how the "same" foods differ across countries and continents, revealing the invisible ingredients that can significantly impact our health.

## Overview

This project combines personal narrative with data analysis to explore conscious eating in a globalized world. After moving from Italy to the United States and experiencing unexpected health issues while eating the "same" diet, this story investigates the hidden differences in food products across five countries representing five continents.

## The Story

Starting with a personal journey, this interactive narrative explores:
- How identical-looking foods differ dramatically in ingredient composition across countries
- The complexity of food products measured by ingredient counts and additive usage
- Regional patterns in food manufacturing and processing
- The importance of transparency in food labeling and production

Through interactive data visualizations, users can explore specific foods, compare products across countries, and discover patterns in global food systems.

## Data

### Countries Analyzed
- 🇺🇸 **United States** (Americas)
- 🇮🇹 **Italy** (Europe)
- 🇿🇦 **South Africa** (Africa)
- 🇯🇵 **Japan** (Asia)
- 🇳🇿 **New Zealand** (Oceania)

### Dataset
- **50 food categories** representing staple foods worldwide
- **2,000+ products** across all five countries
- **Data source**: [Open Food Facts](https://world.openfoodfacts.org/) API
- **Collection period**: November 2025
- **Format**: JSON (included in repository)

Countries were selected based on data availability and language accessibility. The dataset underwent extensive cleaning and normalization (see [METHODOLOGY.md](METHODOLOGY.md) for details).

### Key Metrics
- Number of ingredients per product
- Food category complexity scores
- Types and counts of additives used
- Cross-country dietary comparisons

## Features

### Interactive Visualizations
All visualizations are created using [Observable Framework](https://observablehq.com/) and embedded in the site:
- **Search & Filter**: Find specific foods by name or category
- **Comparison Tools**: Side-by-side country comparisons
- **Before/After Views**: Explore product differences
- **Network Visualizations**: Ingredient and additive relationships
- **Exploratory Data Tools**: User-driven data investigation

### Accessibility
- ♿ **WCAG Compliant**: Meets Web Content Accessibility Guidelines
- **Alt Text**: All visualizations include descriptive alternative text
- **Keyboard Navigation**: Full site navigability without mouse
- **Screen Reader Support**: Semantic HTML and ARIA labels

## Technology Stack

- **HTML/CSS/JavaScript**: Core web technologies
- **Observable Framework**: Data visualizations via embeds
- **Responsive Design**: Mobile-first, centered content layout
- **Static Site**: Pure client-side, no server required

## Getting Started

### Prerequisites
- Modern web browser
- Git (for cloning repository)

### Local Development

1. Clone the repository:
```bash
git clone https://github.com/avgelix/what_do_you_eat.git
cd what_do_you_eat
```

2. Open in browser:
```bash
"$BROWSER" index.html
```

That's it! No build process required.

## Project Structure

```
what_do_you_eat/
├── index.html              # Main story page
├── styles/                 # CSS stylesheets
├── scripts/                # JavaScript files
├── assets/                 # Images and illustrations
├── data/                   # Cleaned dataset (JSON)
├── README.md               # This file
├── METHODOLOGY.md          # Data collection and cleaning process
└── LICENSE                 # License information
```

## Deployment

This site can be hosted on:
- **GitHub Pages**: Automatic deployment from `main` branch
- **Vercel**: Zero-config deployment
- **Any static host**: Upload files to any web server

### Custom Domain
Custom domain configuration instructions will be added after domain setup.

## Contributing

While this is a solo project, contributions are welcome in the form of:
- Bug reports and fixes
- Accessibility improvements
- Typo corrections
- Translation suggestions

Please open an issue or pull request on GitHub.

## Call to Action

This project wouldn't be possible without [Open Food Facts](https://world.openfoodfacts.org/), a free, open, and collaborative database of food products from around the world.

**You can help make food transparency better:**
1. Download the [Open Food Facts app](https://world.openfoodfacts.org/open-food-facts-mobile-app)
2. Scan products you buy
3. Add or verify product information
4. Contribute to a global public database

Every contribution helps researchers, consumers, and projects like this one understand what we really eat.

## Data Sources & Credits

- **Data**: [Open Food Facts](https://world.openfoodfacts.org/) - Open Database License (ODbL)
- **Analysis & Visualization**: Original work by avgelix
- **Development Environment**: Ubuntu 24.04.3 LTS

## Methodology

For detailed information about data collection, cleaning, and analysis processes, see [METHODOLOGY.md](METHODOLOGY.md).

## License

This project uses dual licensing:

- **Code** (HTML, CSS, JavaScript): [MIT License](LICENSE)
- **Content & Documentation**: [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)

You are free to:
- Use the code in your own projects
- Adapt and build upon the content
- Share the visualizations and findings

Attribution required for content reuse.

## Contact

- **Repository**: [github.com/avgelix/what_do_you_eat](https://github.com/avgelix/what_do_you_eat)
- **Issues**: [Report a problem or suggestion](https://github.com/avgelix/what_do_you_eat/issues)

---

*Building awareness, one ingredient at a time.*