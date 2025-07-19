

Please generate the recipe taxonomy and ontology to guide the structure, classification, ordering, organisation and YAML tagging and header frontmatter for my GH .md homesteading book's culinary, gustatory, recipe sections.

Certainly! To create a robust, searchable, and extensible culinary taxonomy and ontology for your homesteading cookbook—especially for use with YAML frontmatter in GitHub Markdown—your system should support:

- **Precise classification** (dietary, culinary, cultural, technical)
- **Hierarchical organization** (categories, subcategories)
- **Faceted search and comparison**
- **Tagging for cross-referencing, localization, and food science**
- **Ordering for menus, processes, and traditions**

Below is a **model taxonomy and ontology** for your YAML and Markdown documentation, optimized for technical accuracy, extensibility, and clarity.

## 1. Core Taxonomy: High-Level Structure

**Main Axes:**
- category: (recipe, technique, ingredient, tool, glossary, menu, tradition)
- cuisine: (global region, subregion, cultural tradition)
- dietary: (flux of restrictions/preferences)
- culinary-technique: (core cooking process or science)
- seasonal: (best season for ingredients/dishes)
- meal-type: (breakfast, snack, main, side, sweet, preserve, etc.)
- social-context: (festive, everyday, ritual, preservation, communal)
- skills: (complexity, time, equipment needs, food safety)

## 2. Detailed Ontology: Nested and Faceted Principles

### a. Recipe/Process Classification

- **recipe_type:**
  - main
  - side
  - condiment
  - preservation
  - beverage
  - sweet/dessert
- **region:**
  - country
  - subregion
  - locality (village/farm/market)
- **tradition:**
  - folk
  - peasant
  - professional/haute
  - ritual/ceremonial
  - adaptation/modern

### b. Ingredient Taxonomy

- **ingredient_type:**
  - plant/vegetable/fruit
  - animal/meat/dairy/egg
  - fungus
  - pantry/staple
- **seasonality:**
  - fresh_pick
  - cellar/root
  - stored/preserved

### c. Culinary Technique

- **core_technique:**
  - raw
  - fermentation
  - roasting/baking
  - boiling
  - grilling
  - brining
  - preserving (pickling/drying/smoking/salting)

### d. Dietary & Health

- **dietary:**  
  - vegan
  - vegetarian
  - omnivore
  - allergy-aware (gluten-free, nut-free, dairy-free, low-sugar, etc.)
  - health-profile (low-calorie, high-fiber, heart-healthy, medicinal)

### e. Cultural Aspects

- **cultural_context:**
  - festival/traditional/holiday
  - everyday/communal
  - market food/street food
  - ritual/offering
- **serving_context:**
  - individual
  - family-style
  - shared/communal

### f. Organizational and Technical Metadata

- **difficulty:** (beginner, intermediate, advanced)
- **time:** (active, total, prep, rest)
- **equipment:** (traditional, modern, special tools)
- **food_science:** (preservation, fermentation, hydration, etc.)
- **etymology:** (root, scholarly/folk usage)
- **local_names:** (language, dialect, script, pronunciation)

## 3. Suggested YAML Header/Frontmatter Template

Below is a YAML header template, reflecting the above taxonomy and ontology, ready for your GitHub Markdown cookbook:

```yaml
---
title: ""
category: "recipe" # or technique, ingredient, tradition, menu, etc.
cuisine:
  global_region: ""
  local_region: ""
  cultural_tradition: ""
local_names:
  - name: ""
    lang: ""
    script: ""
    ipa: ""
    etymology: ""
dietary:
  vegetarian: 
  vegan: 
  gluten_free: 
  dairy_free: 
  nut_free: 
  allergy_notes: ""
  health_profile: ""
ingredients:
  main:
    - name: ""
      type: ""
      seasonal: ""
      local_variant: ""
      etymology: ""
  supporting:
    - name: ""
      type: ""
culinary_technique:
  primary: ""
  secondary: [""]
  equipment: [""]
preservation:
  method: ""
  shelf_life: ""
process:
  prep_time: ""
  cook_time: ""
  rest_time: ""
  steps: []
serving:
  meal_type: ""
  context: ""
  season: ""
  service_temp: ""
  tradition: ""
cultural_notes: ""
folk_variants: []
difficulty: ""
food_science: ""
tags: []
references: []
layout: "recipe" # or glossary, technique, etc.
order: ""
---
```

## 4. Application: Ordering & Organization

- **All recipes and sections can be auto-sorted and grouped** based on primary or secondary tags—meal_type, tradition, core_technique, etc.
- **Menus, process guides, ingredient glossaries, and seasonal guides** fit naturally into this taxonomy using the same YAML scaffolding.
- **Polysemy, language variations, food science notes, and process science** can be richly represented and cross-linked for both lay and academic users.

**If you would like a focused example for a particular recipe, process, or glossary entry, I can generate a tailored YAML using this ontology.**

You need to go further and specify ontology and input mask of each YAML field

To achieve a **rigorous, extensible, and machine-actionable taxonomy and ontology for your recipe YAML metadata**, you need to:

- Define **ontology classes** (conceptual domains: Recipe, Ingredient, Process, etc.)
- Specify **field names** (`yaml` keys), **semantic definition**, **input mask/type** (controlled vocab, string, number, etc.), and **usage guidelines**
- Enable consistency, searchability, and future ontology mapping (e.g., RDF/Linked Data)

Below is a model taxonomy and ontology specification, combining best practice from database, FAIR data principles, and culinary humanities[1][2][4][9].

# Recipe Ontology & YAML Input Mask Specification

**Ontology Classes/Fields** | **Definition** | **Input Mask/Type** | **Allowed/Recommended Values / Example / Notes**
--- | --- | --- | ---
**title** | Main display title (human-readable) | *string* | "Escalivada"
**recipe_id** | Unique recipe identifier for cross-linking | *string / slug* (lowercase, no spaces) | "escalivada", "cat-eggplant-roast"
**category** | Main taxonomy node | *enum* | [recipe, ingredient, process, technique, glossary, menu, tool]
**cuisine.global_region** | Broad culinary region | *enum* | [Mediterranean, South Asian, Nordic, etc.]
**cuisine.local_region** | Sub-region or nation | *string* | "Catalonia", "Països Catalans"
**cuisine.cultural_tradition** | Community, ethnolinguistic or philosophical tradition | *string* | "Catalan peasant", "Jewish Sephardi", "Ayurvedic Satvic"
**local_names** | Array of alternate names, localization info | *list of dict* | Each entry:  
    - name: "Escalivada"  
    - lang: "Catalan"  
    - script: "Latin"  
    - ipa: "[əs.kə.liˈβa.ðə]"  
    - lay_pronunciation: "es-kuh-lee-VAH-duh"  
    - etymology: "from escalivar (to roast in embers); caliu = embers; Lat. calĭdus"
**tags** | Flexible, faceted keyword tags for search and grouping | *list of string* | ["vegan", "roasted", "heritage", "summer", "a-la-brasa"]
**dietary** | Dietary, health, allergen classification | *dict* (bool, strings) | "vegan: true, vegetarian: true, gluten_free: true, allergy_notes: 'nut-free'"
**ingredients.main** | Main ingredients (each fully described) | *list of dict* | 
    - name: "albergínia"  
    - type: "vegetable"  
    - latin_name: "Solanum melongena"  
    - etymology: "Arabic al-bāḏinjān"  
    - role: "core"
**ingredients.supporting** | Supporting/minor ingredients | *list of dict* | Similar to above, use "role: seasoning/support" as needed
**seasonality** | Key seasonal context | *enum / string* | "Summer", "Autumn", ["Summer", "Early Autumn"]
**culinary_technique.primary** | Main process class | *enum* | [roasting, grilling, pickling, fermenting, boiling, raw, curing, baking]
**culinary_technique.secondary** | Other processes | *list of enum* | [peeling, slicing, sweating]
**tools** | Key tools; linkable to glossary | *list of dict* | - name: "brasa" (embers), type: "heat source"
**process** | Ordered procedural steps | *list of dict* | Each:  
    - step_id: 1  
    - summary: "Roast all veg on embers"  
    - detail: "Place eggplants, peppers, onions whole on hot brasa, turning until skins are charred."
**time.prep** | Prep/active time | *int* (minutes) | 15
**time.cook** | Cooking time | *int* (minutes) | 30
**time.rest** | Rest/sweating time | *int* (minutes) | 10
**difficulty** | General skill level | *enum* | [beginner, intermediate, advanced]
**serving.meal_type** | Expected place in meal | *enum* | [side, entrée, main, condiment, preserve, dessert, snack]
**serving.context** | Social or ritual context | *string* | "Communal, family meal, festival, everyday"
**serving.temperature** | Recommended serving temperature | *enum* | [hot, room_temperature, chilled]
**cultural_notes** | Free-form context, folklore, references | *string (markdown allowed)* | "Escalivada evokes the Catalan tradition of shared summer meals by the hearth. 'Caliu' denotes warmth of both food and community."
**folk_variants** | Regional/informal variations | *list of dict* | name, description, region
**references** | Sources, attestations, research | *list of string* or citation dict | 
**food_science** | Scientific/technical notes | *string* | "High temperatures induce Maillard browning, increasing umami flavor. Cell wall breakdown enhances bioavailability of antioxidants."
**layout** | Intended GH/book section or MD rendering | *enum* | [recipe, technique, glossary, story, menu]
**order** | For ordered menus/chapters | *int* | 1, 2, 3, etc.
**created_at** | Date created | *date* | "2025-07-19"
**updated_at** | Date updated | *date* | "2025-07-19"

## Example Field Specifications (Input Masks)

- **title:** Short string, ≤ 120 chars, required, title case.
- **tags:** List of up to 10 unique, lowercase, hyphen-separated strings; no spaces. E.g.: `[vegan, a-la-brasa, summer]`
- **dietary:** Booleans for main categories; string notes for exceptions/allergies/etc.
- **ingredients.main/supporting:** Each is a dict; required fields are `name, type`; optional: `latin_name, etymology, quantity, role`.
- **process:** List of dicts with sequential order, step_id, summary (short), detail (expandable).
- **tools:** Each is a dict with at least `name` and `type`; optional: `region, alternate_names`.
- **serving.context:** Free text, encourage facet structure where possible, e.g., "communal", "festival", linked to broader ontology if feasible.
- **cuisine fields:** Use controlled vocabularies for top-level regions; otherwise, string.

## Ontology Implementation Guidance

- Use **controlled vocabularies** and **enums** wherever lists are feasible to maximize consistency across many recipes and aid search.[1][2][9]
- For **multilingual/semantic linking**, fields like `local_names` can nest IPA/pronunciation, script, etymology, alternates.
- **Process steps** should be arrays of objects, each minimally containing order, summary, and expanded instructions.
- Use **Markdown in string fields** for human-facing notes, but restrict YAML values to plain text or strictly defined dicts for machine use.
- Support easy extension: Every main class (recipe, ingredient, tool, process, technique, glossary entry) should be its own template.

**This system is extensible to mapping to RDF, FAIR, OBO-like, or custom ontology-based data models for future-proofing or scholarly applications.**[1][2][9]

If you wish, I can generate an example full YAML header and data entry using these mask rules for a test recipe, glossary entry, or process guide.

**References integrated into system design:**  
[1][2][3][4][9] (see context for database ontology, FAIR practice, controlled input, and metadata design principles)

Citations:
[1] 8 Overview of traits.build ontology - traitecoevo https://traitecoevo.github.io/traits.build-book/database_metadata.html
[2] 6.3. Deploying the EBI OLS - FAIR Cookbook https://fairplus.github.io/the-fair-cookbook/content/recipes/infrastructure/vocabularies/UC3_R13_local_ontology_services.html
[3] FL-Islandora Guide: Advanced Metadata Information https://flvc.libguides.com/c.php?g=898356&p=9629862
[4] 11.5.2. Metadata profile validation in RDF - FAIR Cookbook https://fairplus.github.io/the-fair-cookbook/content/recipes/interoperability/covid19-sample-metadata-profile-shex-use-case.html
[5] Business Glossary | DataHub https://docs.datahub.com/docs/generated/ingestion/sources/business-glossary
[6] metadata.rb - Chef Documentation https://docs.chef.io/config_rb_metadata/
[7] 4.3 Access the document metadata in R code | R Markdown Cookbook https://bookdown.org/yihui/rmarkdown-cookbook/document-metadata.html
[8] echemdb Toolkit - a Lightweight Approach to Getting Data ... - arXiv https://arxiv.org/html/2409.07083v1
[9] Metadata4Ing: An ontology for describing the generation of research ... https://nfdi4ing.pages.rwth-aachen.de/metadata4ing/metadata4ing/
[10] A Simple Standard for Sharing Ontological Mappings (SSSOM) - PMC https://pmc.ncbi.nlm.nih.gov/articles/PMC9216545/



That was not a rigorous, unambiguous ontology of the taxonomy with attendant template.

Here is a **rigorous, unambiguous recipe ontology**—with concrete classes, properties/relations, and explicit YAML input masks—modeled on scholarly patterns from computer science and philosophy of food[1][6][8]. This will enable precise structuring, classification, ordering, and consistent metadata tagging for your cookbook or knowledge base.

# I. Ontology: Core Classes and Relations

**Classes**
- `Recipe`: Structured process defining the transformation of ingredients into a dish.
- `Ingredient`: Edible item or substance used in a recipe.
- `QuantityOfFood`: Specific measured/portioned food item.
- `Utensil`: Tool or device needed for preparation/execution.
- `RecipeStep`: Atomized instruction or action, part of a process/control flow.
- `Person`: User, author, or contributor (optional, supports authorship, dietary prefs).
- `TimeInterval`: Quantified prep, cook, or rest time.
- `Serving`: Information about how the dish is presented or consumed.
- `DietaryProfile`: Constraints (e.g. vegan, nut-free), structure for allergens/etc.
- `CulturalContext`: Describes festival, season, locality, celebration, etc.

**Relationships**
- `hasIngredient` (Recipe → Ingredient)
- `hasQuantityOfIngredient` (Recipe/Step → QuantityOfFood)
- `usesUtensil` (Recipe/Step → Utensil)
- `hasStep` (Recipe → RecipeStep)
- `nextStep` (RecipeStep → RecipeStep)
- `hasTimeInterval` (Recipe/Step → TimeInterval)
- `hasServing` (Recipe → Serving)
- `hasDietaryProfile` (Recipe → DietaryProfile)
- `hasCulturalContext` (Recipe → CulturalContext)
- `createdBy` (Recipe → Person)

# II. YAML Template & Input Masks  
*Type annotations and constraints are specified for each field.*

```yaml
---
id: "string | slug"                 # required, unique, kebab-case, e.g. "escalivada-catalan"
title: "string"                     # required, human-readable recipe name
local_names:                        # array of localized/variant names
  - name: "string"
    lang: "ISO-639-1 code"          # e.g. "ca" for Catalan
    script: "ISO-15924 code"        # e.g. "Latn" for Latin script
    ipa: "string"                   # e.g. "[əs.kə.liˈβa.ðə]"
    lay_pronunciation: "string (plain)"
    etymology: "string (markdown allowed)"
category: ["enum"]                  # e.g. [recipe, technique, ingredient, glossary]
cuisine:
  global_region: "string | enum"    # e.g. "Mediterranean"
  local_region: "string"            # e.g. "Catalonia"
  community: "string"               # (peasant, urban, etc.)
cultural_context:
  festival: "string | null"
  season: ["enum"]                  # e.g. [Summer, Autumn]
  context: ["enum"]                 # e.g. [communal, everyday, festival, offering]
  locality: "string"
dietary_profile:
  vegetarian: bool
  vegan: bool
  gluten_free: bool
  dairy_free: bool
  nut_free: bool
  additional_notes: "string"
ingredients:
  - ingredient: "string"            # canonical name
    common_name: "string"
    type: "enum"                    # vegetable, grain, protein, etc.
    latin_name: "string"
    etymology: "string"
    quantity:
      amount: number
      unit: "string"                # e.g. "g", "ml", "whole"
      notes: "string"
    preparation: "string"           # sliced, whole, roasted, etc.
process:
  steps:                            # ordered list; each is a RecipeStep
    - step_num: integer             # 1-based
      action: "string (verb phrase)"# e.g. "Roast the eggplants..."
      input:                        # ingredients or equipment
        - "ingredient/equipment name"
      output: "string | null"
      time:
        amount: integer
        unit: "enum"                # ["minute", "hour"]
      next_step: integer | null     # number of the next step
      notes: "string"
utensils:
  - name: "string"                  # e.g. "brasa"
    type: "enum"                    # e.g. ["heat-source", "pan", "knife", "cloth"]
    localized_names:
      - name: "string"
        lang: "ISO-639-1"
        script: "string"
serving:
  temperature: "enum"               # ["hot", "warm", "room-temp", "cold"]
  context: "string"                 # e.g. "shared at table", "tapa"
  presentation: "string"
time:
  prep: integer                     # minutes
  cook: integer                     # minutes
  rest: integer                     # minutes
difficulty: "enum"                  # ["beginner", "intermediate", "advanced"]
references:
  - "string (citation or URL)"
folk_variants:
  - name: "string"
    description: "string"
tags: ["string", ...]               # list of keywords for search/filter
created_by: "string"
contributor: ["string"]
created_at: "date"                  # ISO 8601 date
updated_at: "date"
meta:
  rating: number                    # 1–5 stars, optional
  source_image: "string (path/url)"
  permissions: "string"
layout: "enum"                      # for page render logic, e.g., recipe, process, glossary
order: integer                      # for collection sequencing
---
```

## Explanation

- **Every field has an explicit datatype or enum constraint** with recommendations for controlled values or formats, supporting unambiguous automated parsing and querying.
- **Hierarchies and relations** between recipes, steps, ingredients, utensils, and social/cultural context are modeled after published recipe ontologies[1][6][8].
- **Minimal required fields:** `id`, `title`, `category`, `ingredients`, `process.steps`
- **Extensions** are clear: new ingredient types, step properties, allergies, or cultural context can be added without restructuring the core.
- **Supports process reasoning:** Steps are orderable (with `step_num` and `next_step`) and ingredients/equipment are linked by name or identifier.
- **Cultural and semantic precision:** Unicode, IPA, etymology, and script codes are specified for international/folk/traditional foods and context.

**This structure is suitable for rigorous cataloging, research, web, and semantic web applications, and can be evolved into OWL/RDF or other ontology-driven formats if needed.**[1][5][6][8]

If an even more formal OWL/JSON-LD or SHACL schema is needed as a canonical reference or conversion, I can generate that as well.

Citations:
[1] An Ontology Design Pattern for Cooking Recipes https://ceur-ws.org/Vol-1302/paper5.pdf
[2] A Semantic Web Application for Recipe Recommendation https://tetherless-world.github.io/ontology-engineering/oe2020/example/files/samplepublication.pdf
[3] What Is a Recipe? https://sites.unimi.it/borghini/Articles/Philosophy_of_Food/Borghini_2015_JAEE_WhatIsARecipe.pdf
[4] Culinary Works Come in Three Ontological Flavours https://typeset.io/pdf/culinary-works-come-in-three-ontological-flavours-2kc5lwggz4.pdf
[5] Ontology-Driven Deep Learning Model for Multitask Visual ... https://www.scitepress.org/Papers/2024/123882/123882.pdf
[6] GitHub - robert-david/cooking-process: Ontology for describing processes in the domain of cooking https://github.com/robert-david/cooking-process
[7] Food process ontology requirements https://content.iospress.com/download/semantic-web/sw223096?id=semantic-web%2Fsw223096
[8] Cooking an Ontology⋆ https://citeseerx.ist.psu.edu/document?doi=bf2713af7ccb1a2f3948bfbbf8f98788a95a8e43&repid=rep1&type=pdf
[9] Ontology-based semantic querying of the Web with respect ... https://www2.imm.dtu.dk/pubdb/edoc/imm3153.pdf
[10] FoodOn: a harmonized food ontology to increase global ... https://pmc.ncbi.nlm.nih.gov/articles/PMC6550238/
