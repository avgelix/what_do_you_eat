# Methodology

This document details the data collection, cleaning, and analysis process used in the "What Do You Eat" project.

## Research Question

How do food products with similar labels and purposes differ in ingredient composition across countries on different continents?

## Hypothesis

Foods that appear identical across countries often contain significantly different ingredients, additives, and levels of processing that can impact health outcomes.

## Data Collection

### Source
All product data was collected from the [Open Food Facts](https://world.openfoodfacts.org/) API in **November 2025**.

Open Food Facts is a collaborative, free, and open database of food products from around the world, created by volunteers who scan and upload product information.

### Country Selection

Five countries were chosen to represent five continents:

| Continent | Country | Rationale |
|-----------|---------|-----------|
| Americas | United States | Large database, high product diversity |
| Europe | Italy | Language accessibility (native speaker), strong food culture |
| Africa | South Africa | Best data availability among African countries |
| Asia | Japan | Extensive product documentation, distinct food culture |
| Oceania | New Zealand | Good data coverage, English language |

**Selection criteria:**
1. Data availability and completeness
2. Language accessibility for manual review
3. Geographic representation
4. Product diversity

### Food Categories

50 staple food categories were identified representing common foods consumed globally across different food groups:
- Grains and cereals
- Dairy products
- Proteins (meat, fish, legumes)
- Fruits and vegetables (fresh and processed)
- Condiments and sauces
- Beverages
- Snacks and desserts
- Cooking ingredients

[*List of all 50 categories to be added*]

### Data Retrieval

For each country and food category:
1. Queried Open Food Facts API using category tags and country filters
2. Retrieved up to 20 representative products per category
3. Extracted: product name, ingredients list, additives, nutrition facts, labels

**Target**: 50 categories × 5 countries × 20 products = 5,000 products
**Actual**: ~2,000 products after filtering for completeness

## Data Cleaning Process

The raw data required extensive cleaning to ensure comparability across countries. This was a multi-step, iterative process.

### 1. Language Translation

**Challenge**: Ingredient lists were in multiple languages based on product origin and market.

**Languages encountered**: English, Italian, French, Spanish, German, Dutch, Portuguese, Japanese, Afrikaans, Zulu, Māori, and others (15+ total).

**Process**:
- Manual translation of all non-English ingredient lists to English
- Verified translations using multiple sources
- Standardized terminology (e.g., "maize" → "corn", "courgette" → "zucchini")
- Created a translation glossary for consistency

### 2. Additive Code Normalization

**Challenge**: Additives listed inconsistently across countries:
- E-numbers (Europe): "E330"
- Names only: "Citric acid"
- Country-specific codes: "INS 330" (International Numbering System)
- Mixed formats: "E330 (citric acid)"

**Process**:
1. Created comprehensive mapping table of additive codes:
   - E-numbers ↔ INS numbers ↔ Common names ↔ Chemical names
2. Standardized all additives to E-number format with parenthetical common name
3. Verified additive functions and safety classifications
4. Tagged additives by purpose (preservative, colorant, emulsifier, etc.)

**Example transformations**:
```
"citric acid" → "E330 (Citric acid)"
"INS 330" → "E330 (Citric acid)"
"acidulant (citric acid)" → "E330 (Citric acid)"
```

### 3. Ingredient List Cleaning

**Manual review of every ingredient list** to:
- Remove formatting artifacts (asterisks, percentages in wrong places)
- Standardize delimiters (commas vs. semicolons)
- Parse nested ingredients (e.g., "flour (wheat, barley)")
- Identify and separate sub-ingredients from main ingredients
- Flag ambiguous terms for further research

**Specific issues addressed**:
- Parenthetical clarifications: "(from milk)" vs. actual sub-ingredients
- Compound ingredients: How to count "tomato sauce (tomatoes, salt, spices)"
- Percentage declarations: Preserved when meaningful, removed when formatting noise
- Allergen markers: Standardized bold/caps/underline conventions

### 4. Data Validation

Quality checks performed:
- ✓ All products have complete ingredient lists
- ✓ No duplicate products within same country/category
- ✓ All additives validated against approved databases
- ✓ Ingredient counts verified (min/max ranges checked)
- ✓ Cross-referenced suspicious outliers manually

### 5. Comparability Adjustments

To enable fair cross-country comparisons:
- Excluded products with incomplete data (main cause of reduced dataset size)
- Standardized serving sizes and units where possible
- Created normalized ingredient complexity scores
- Categorized products into processing levels (minimal, moderate, ultra-processed)

## Data Structure

Final cleaned dataset stored as JSON with schema:

```json
{
  "product_id": "string",
  "product_name": "string",
  "country": "string",
  "category": "string",
  "ingredients": ["array of strings"],
  "ingredient_count": "number",
  "additives": [
    {
      "code": "string (E-number)",
      "name": "string",
      "function": "string"
    }
  ],
  "additive_count": "number",
  "processing_level": "string",
  "complexity_score": "number",
  "source_url": "string (Open Food Facts link)"
}
```

## Analysis Methods

### Metrics Calculated

1. **Ingredient Count**: Total number of distinct ingredients per product
2. **Additive Count**: Number of E-coded additives per product
3. **Category Complexity**: Average ingredient count per food category
4. **Additive Diversity**: Unique additives used across products
5. **Cross-Country Comparison**: Same category across different countries

### Statistical Approaches
[*To be expanded based on specific analyses performed*]

## Limitations

### Data Limitations
- **Voluntary reporting**: Open Food Facts relies on community contributions; coverage varies by country
- **Temporal snapshot**: Data from November 2025; products change over time
- **Sample bias**: More popular/accessible products overrepresented
- **Language barrier**: Some nuance may be lost in translation despite careful review

### Methodological Limitations
- **Category definitions**: Some products fit multiple categories
- **Serving size variations**: Not all products directly comparable by quantity
- **Missing data**: Products without complete ingredient lists excluded
- **Processing classification**: Subjective assessment of processing levels

### Geographic Limitations
- Only 5 countries analyzed; not representative of entire continents
- Countries chosen partly for data availability, not random selection
- Urban vs. rural product availability not distinguished

## Reproducibility

### To Reproduce This Analysis

1. **Data Collection**:
   ```bash
   # Query Open Food Facts API
   curl "https://world.openfoodfacts.org/cgi/search.pl?search_terms=CATEGORY&countries_tags=COUNTRY&json=1"
   ```

2. **Data Cleaning**:
   - Use translation glossary (to be published separately)
   - Apply additive mapping table (to be published separately)
   - Follow standardization rules documented above

3. **Analysis**:
   - Code and notebooks available in Observable collection
   - Dataset available in `/data` directory

### Tools Used
- Open Food Facts API
- Manual data review and cleaning
- Observable Framework for visualization
- Standard web technologies (HTML/CSS/JavaScript)

## Future Work

Potential extensions to this methodology:
- Expand to more countries and regions
- Longitudinal analysis (track changes over time)
- Include nutritional metrics alongside ingredients
- Automated translation and cleaning pipelines
- Machine learning for processing level classification

## Acknowledgments

This analysis was made possible by the thousands of Open Food Facts contributors worldwide who voluntarily scan, photograph, and document food products.

## Questions or Suggestions?

If you have questions about the methodology or suggestions for improvement, please [open an issue](https://github.com/avgelix/what_do_you_eat/issues) on GitHub.

---

*Last updated: December 2025*