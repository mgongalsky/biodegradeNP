# Functional Specification
## Interactive Website for Porous Silicon Biodegradation Modelling

**Document type:** Product / functional requirements specification  
**Purpose:** Define what the website must do from the user’s point of view, without prescribing the mathematical algorithms, numerical methods, software architecture, libraries, frameworks, or implementation details.  
**Status:** Working master specification  
**Scope:** Interactive companion website for a scientific article on biodegradation / dissolution of porous silicon and related porous nanomaterials.

---

# 1. Product vision

The website is an interactive scientific companion to the article. Its purpose is not merely to reproduce figures from the paper, but to allow a reader or experimental researcher to:

1. understand the physical logic of the biodegradation model;
2. inspect experimental datasets from the literature together with model descriptions / fits;
3. upload their own degradation data and analyse them using simplified limiting models;
4. compare those simplified descriptions with the complete model;
5. explore how assumed particle and experimental parameters affect predicted degradation;
6. design hypothetical particles with approximately desired degradation behaviour;
7. trace model assumptions and parameter dependencies back to supporting experimental examples.

The intended conceptual user journey is:

> **Learn → Inspect evidence → Analyse your data → Explore the full model → Design a particle**

The website should work as a scientific tool first and as a visual supplement to the paper second.

---

# 2. Core design principles

## 2.1 Scientific clarity

The interface must distinguish clearly between:

- experimental measurements;
- fitted curves;
- model predictions;
- limiting approximations;
- full-model calculations;
- user-entered assumptions;
- values inferred from data;
- literature-derived parameter relationships.

The user must always be able to understand where a displayed value came from.

## 2.2 Progressive complexity

The site should not expose the most complicated workflow immediately.

A new user should be able to:

1. browse examples without configuring anything;
2. perform a simple fit with minimal inputs;
3. enter the full-model workflow only if needed;
4. use the design sandbox when they want predictive exploration.

## 2.3 Reproducibility

Any calculated result that matters scientifically should be exportable together with enough metadata to reconstruct what was shown.

## 2.4 Evidence-backed modelling

Where the website uses empirical dependencies on factors such as particle properties, treatment conditions, environment, or coating, the user should be able to inspect the experimental examples supporting those dependencies.

## 2.5 No false precision

The interface should distinguish:

- directly measured values;
- fitted effective parameters;
- inferred physical parameters;
- assumed parameters;
- extrapolated predictions.

Predictions outside the range supported by the available examples should be marked clearly.

## 2.6 Practical rather than purely demonstrative

The site should help an experimentalist answer questions such as:

- Does a limiting model describe my degradation curve adequately?
- What characteristic degradation timescale does my experiment imply?
- Would the complete model behave differently?
- Which parameter is most likely responsible for a mismatch?
- What degradation behaviour should I expect for a particle with chosen properties?
- What approximate particle parameters could give me a target degradation time?

---

# 3. High-level site structure

The final navigation should contain five principal sections:

1. **Home / Welcome**
2. **Theory**
3. **Examples**
4. **Your Particle**
5. **Design Your Nanoparticle**

The final position of **Theory** in the navigation is second, even though it should be implemented late in the development roadmap.

Possible working names may change during UI design, but the functional separation should remain.

---

# 4. Global website requirements

## 4.1 Main navigation

The user must be able to switch between all major sections without losing the overall context of the site.

The navigation should make clear which section is currently active.

## 4.2 Responsive layout

The website should remain usable on:

- standard desktop monitors;
- laptops;
- tablets;
- mobile devices for reading and basic inspection.

Advanced graph manipulation and fitting workflows may be optimised primarily for desktop, but must not become unusable on smaller screens.

## 4.3 Consistent scientific terminology

The same terms, units, symbols, and parameter names must be used consistently across:

- Theory;
- Examples;
- fitting workflows;
- full-model calculations;
- design sandbox;
- exports.

## 4.4 Units

Whenever quantities carry units:

- units must be displayed explicitly;
- the user should not have to infer them from context;
- if unit conversion is supported, the selected display/input unit must remain visible;
- exported results must contain units.

## 4.5 Parameter provenance

For every parameter shown in a calculation, the interface should identify its status where relevant:

- user supplied;
- imported from example;
- fitted;
- calculated;
- fixed default;
- literature derived.

## 4.6 Validation and warnings

The interface must detect obvious invalid inputs such as:

- missing required columns;
- non-numeric values in numeric data columns;
- impossible percentages;
- invalid time ordering;
- invalid parameter ranges;
- inconsistent units;
- empty datasets;
- insufficient data for fitting.

Warnings should be informative and should not silently modify scientific data.

## 4.7 Session state

Within a working session, navigating between views should preserve the user’s current data and parameter selections where practical.

For example:

- a dataset loaded in **Your Particle** should not disappear because the user briefly visits **Examples**;
- a literature example loaded into the design sandbox should preserve its imported parameters while the user experiments.

## 4.8 Reset controls

Every interactive scientific workflow should have a clear way to:

- reset only the current plot/view;
- restore original example values;
- clear an uploaded dataset;
- reset the full workflow to defaults.

---

# 5. Home / Welcome

## 5.1 Purpose

The Home page should explain, briefly and visually, what the website is and what a visitor can do with it.

It should not reproduce the full theory.

## 5.2 Required content

The page should communicate:

- that the website accompanies a scientific model of porous-material biodegradation / dissolution;
- that dissolution and transport are the central physical processes;
- that the site includes literature examples, data fitting, full-model exploration, and virtual particle design;
- that users can browse without uploading any data.

## 5.3 Suggested entry points

The Home page should provide prominent actions such as:

- **Browse Examples**
- **Analyse My Data**
- **Design a Particle**
- **Read the Theory**

## 5.4 Article connection

The page should contain a clearly identifiable location for:

- article title;
- authors;
- publication / DOI link when available;
- citation information.

This information may initially be placeholder content until the article metadata is final.

## 5.5 Minimal first implementation

For the earliest layout-only MVP, Home may contain only:

- title;
- one-paragraph description;
- navigation cards/buttons;
- placeholder article citation;
- non-functional preview cards for the principal tools.

---

# 6. Theory

## 6.1 Purpose

The Theory section should allow a reader to understand the hierarchy of the model from physical intuition to the different solution regimes.

It should be readable independently from the article, but should not attempt to become a full textbook chapter.

## 6.2 Presentation order

The final Theory section should proceed from general concepts to specific models.

### 6.2.1 Physical picture

Explain that a porous particle undergoes two coupled processes:

- dissolution of the solid material;
- transport / diffusion of dissolved species.

### 6.2.2 Effective local description

Explain why the model does not track every microscopic internal pore boundary explicitly.

Introduce the concept that the porous material is represented through:

- local porosity;
- effective local material properties;
- effective reactive surface.

### 6.2.3 General spatial model

Explain that the physical problem can in general be written as a three-dimensional transport-and-source problem.

The site should explain conceptually:

- what varies in space;
- what varies in time;
- what generates dissolved species;
- what transports them;
- how porosity changes as material is lost.

### 6.2.4 Symmetry reduction

For nanoparticles, explain the spherical-particle approximation.

The user should understand that:

- a full 3D problem may be formulated;
- spherical symmetry reduces the problem to radial dependence;
- other geometries may require different symmetry assumptions.

### 6.2.5 Competing characteristic times

Introduce the idea that dissolution and diffusion have characteristic timescales.

### 6.2.6 Limiting regime: fast diffusion

Explain the physical meaning:

- dissolved species are transported rapidly;
- transport does not substantially limit the process;
- observed degradation is predominantly controlled by dissolution.

### 6.2.7 Limiting regime: fast dissolution / diffusion-controlled

Explain the opposite limit:

- dissolution locally proceeds rapidly;
- local accumulation of dissolved species becomes important;
- transport becomes the limiting process.

### 6.2.8 General coupled regime

Explain that when the relevant timescales are comparable, neither limiting approximation is sufficient and the complete coupled model must be solved.

### 6.2.9 Surface-area / porosity closure

Explain why the relationship between accessible reactive surface and porosity is required to obtain a usable model.

Present the supported pore-geometry assumptions conceptually, including:

- cylindrical-pore representation;
- spherical-pore representation.

The exact equations belong in Theory, but this specification intentionally does not prescribe them.

### 6.2.10 Coated particles

Introduce particles with an external barrier layer.

Explain that:

- dissolution occurs in the porous particle;
- the coating introduces an additional transport barrier;
- the coating itself does not necessarily contain the same source term as the dissolving core;
- coating properties can therefore modify the overall degradation kinetics.

## 6.3 Visual requirements

The final Theory section should use diagrams and interactive visual aids where they improve understanding, for example:

- porous particle schematic;
- dissolution + diffusion schematic;
- radial symmetry schematic;
- limiting-regime comparison;
- pore-geometry schematic;
- coated-particle schematic.

These should explain concepts rather than simply decorate the page.

## 6.4 Cross-links

Theory should link naturally to:

- relevant Examples;
- the fitting modes in Your Particle;
- the full-model calculation;
- design parameters in the Sandbox.

For example, a paragraph about a limiting regime may include an action such as **See experimental examples using this regime**.

## 6.5 Development priority

Theory is part of the final product but should be implemented late.

A placeholder page is sufficient during earlier MVP phases.

---

# 7. Examples

## 7.1 Purpose

Examples is an interactive library of experimental datasets used in or relevant to the scientific analysis.

Its job is to show:

- what was measured;
- under what conditions;
- what degradation behaviour was observed;
- how the model describes the data;
- what evidence supports later parameter relationships in the site.

## 7.2 Example catalogue

The user should be able to browse a collection of example cards/rows.

Each example should have at least:

- concise title;
- source/publication;
- one-sentence scientific question;
- material / sample type;
- one or more key experimental factors;
- optional thumbnail / preview graph.

Example titles should be scientific and human-readable, e.g.:

> Effect of oxidation temperature on porous-silicon degradation

rather than internal dataset identifiers.

## 7.3 Search

The catalogue should support text search across appropriate metadata, such as:

- title;
- publication;
- material;
- treatment;
- measurement method;
- experimental condition;
- keywords.

## 7.4 Filtering

The final Examples library should support filters.

Possible filter categories include:

### Material
- porous silicon;
- silica;
- related porous material types.

### Geometry / morphology
- nanoparticle;
- microparticle;
- porous layer;
- other geometry.

### Material properties
- porosity range;
- particle size range;
- pore geometry if known.

### Treatment
- oxidation;
- calcination;
- surface modification;
- coating.

### Environment
- pH;
- temperature;
- solution / buffer type;
- other relevant chemical conditions.

### Measurement
- dissolved silicon;
- remaining silicon;
- silicic-acid concentration;
- other compatible observables.

The final filter vocabulary should be driven by actual dataset metadata.

## 7.5 Individual example page

Opening an example should show a structured detail view.

### Required blocks

1. **Example title**
2. **Short description**
3. **Publication / citation**
4. **Experimental graph**
5. **Model curve(s), where available**
6. **Experimental metadata**
7. **Model / fit metadata**
8. **Source notes / data provenance**
9. **Actions**

## 7.6 Interactive graph

The graph should support:

- display of experimental points;
- display of model curves;
- legend;
- axis labels and units;
- zoom;
- pan where useful;
- reset view;
- hover / point inspection;
- show/hide individual curves or datasets.

The initial Examples MVP does not need cross-example comparison.

## 7.7 Multiple model representations

Where more than one model description exists for an example, the user should eventually be able to toggle individual curves, such as:

- limiting approximation(s);
- complete-model solution;
- alternative assumptions.

The graph must clearly distinguish which curve represents which model.

## 7.8 Experimental metadata

Each example should provide as much structured metadata as the source permits.

Possible fields include:

- sample material;
- particle size;
- particle geometry;
- pore size;
- porosity;
- oxidation / calcination conditions;
- surface chemistry;
- coating;
- particle concentration;
- medium;
- pH;
- temperature;
- incubation conditions;
- sampling times;
- measurement technique;
- measured observable;
- normalisation method;
- source figure/table;
- notes about digitisation or preprocessing.

Missing information should be shown as unavailable rather than guessed.

## 7.9 Model / fit metadata

Where applicable, show:

- which model regime is displayed;
- fitted quantities;
- fixed quantities;
- fit quality metrics where available;
- notes about assumptions.

## 7.10 Publication link

Every literature-derived example must provide a direct and clearly visible reference to its source publication.

## 7.11 Load into other tools

Final Examples pages should support actions such as:

- **Use as starting point in Your Particle**
- **Load into Design Sandbox**

The exact available actions may depend on how complete the example metadata is.

## 7.12 Compare mode — post-MVP enhancement

A later enhancement should allow the user to select datasets/curves from multiple examples and compare them.

Possible comparison behaviour:

- overlay on one graph;
- side-by-side plots;
- optionally normalise selected datasets for comparison;
- show parameter differences next to the graph.

This is explicitly not required for the first Examples MVP.

---

# 8. Your Particle

## 8.1 Purpose

Your Particle is the main analysis workflow for a user who already has experimental degradation data.

The intended workflow is:

> **Import data → Define observable → Quick Fit → Inspect result → Compare with Full Model → Explore/Fit selected parameters → Export**

The page should allow a user to stop after the Quick Fit if that is sufficient.

---

# 9. Data import

## 9.1 Supported input

Initial supported file types:

- CSV;
- generic ASCII / delimited text.

Additional formats may be added later.

## 9.2 Importer behaviour

The importer should support common laboratory data files rather than requiring a single rigid CSV format.

The user should be able to configure:

- delimiter;
- decimal interpretation if necessary;
- whether headers are present;
- number of header lines to skip;
- data columns to use;
- time column;
- measurement column.

## 9.3 Import preview

Before accepting the dataset, show a preview table.

The user should be able to confirm:

- which column is time;
- which column is the measured observable;
- whether parsing was correct.

## 9.4 Observable types

The workflow should initially support at least:

1. fraction / percentage dissolved silicon;
2. fraction / percentage remaining silicon;
3. silicic-acid concentration.

The interface should make clear which observable is being fitted.

## 9.5 Units

The user must specify or confirm:

- time units;
- measurement units where relevant.

If the observable is a percentage or fraction, the site should distinguish between conventions such as:

- 0–1;
- 0–100%.

## 9.6 Data preprocessing controls

Only scientifically transparent preprocessing should be supported.

Potential controls include:

- excluding individual points from fitting without deleting the source data;
- marking points as excluded/included;
- choosing whether data should be normalised where the model requires it.

Any transformation must remain visible in the interface.

The application should preserve the original imported values.

## 9.7 Import errors

The user should receive specific messages for problems such as:

- no numeric data found;
- selected columns have incompatible lengths;
- duplicate/invalid time entries;
- missing measurement values;
- unsupported formatting.

---

# 10. Quick Fit

## 10.1 Purpose

Quick Fit provides a fast, low-complexity analysis using a simplified limiting model.

It is intended to be the default first analysis.

## 10.2 Workflow

After data import:

1. user confirms the observable;
2. site proposes the relevant simple model configuration;
3. user selects the desired limiting case if more than one is available;
4. user starts the fit;
5. site displays the result immediately;
6. fitted curve is overlaid on the experimental data.

## 10.3 Fit configuration

The user should be able to inspect and, where appropriate, change:

- which simplified regime is used;
- which parameters are free;
- which parameters are fixed;
- weighting mode;
- initial assumptions if the interface eventually exposes them.

The initial UI should keep advanced options collapsed.

## 10.4 Weighting

The fit interface should offer a clear choice between supported weighting approaches.

The selected weighting method must be:

- visible;
- included in the exported analysis metadata;
- applied consistently to reported fit metrics.

The product specification does not prescribe the mathematical form of any weighting scheme.

## 10.5 Results

Quick Fit should display:

- fitted curve;
- fitted effective parameter(s);
- characteristic timescale where applicable;
- confidence / uncertainty information if available;
- goodness-of-fit metric(s);
- number of included and excluded points;
- selected fitting assumptions.

## 10.6 Interpretation

The result page should explain what the fitted quantity represents physically.

In particular, it should make clear when the fitted result is an **effective timescale** rather than a uniquely identified microscopic physical constant.

## 10.7 Identifiability warning

Where multiple physical parameters contribute to the same effective fitted quantity, the interface should state that they cannot necessarily be determined independently from a single degradation curve.

## 10.8 Next actions

After Quick Fit the user should be offered:

- **Compare with Full Model**
- **Explore Parameters**
- **Export Result**
- **Reset / Fit another model**

---

# 11. Parameter interpretation / calculator

## 11.1 Purpose

The parameter calculator helps the user relate a fitted effective timescale or effective rate to physical particle/environment parameters.

## 11.2 Typical use case

The user has:

- a fitted effective characteristic time;
- some known experimental parameters;
- one or more unknown or uncertain physical parameters.

The calculator should allow the user to enter the known quantities and inspect what can be inferred about the unknown quantities.

## 11.3 Parameter status

Each parameter should be marked as one of:

- measured / known;
- fitted;
- assumed;
- calculated / inferred;
- not specified.

## 11.4 Supported interaction

The user should be able to:

- fix known parameters;
- change uncertain parameters;
- select a target parameter to calculate where the model permits;
- observe how changes affect the implied characteristic time.

## 11.5 Evidence link

For parameters whose relationships are derived from the site's example database, the interface should offer an action such as:

- **View supporting data**
- **See evidence**

This should open or link to relevant Examples.

## 11.6 Limitations

If a requested inference is non-unique, the interface should not present a single value as uniquely determined.

Instead it may show:

- an admissible range;
- multiple compatible solutions;
- a message that additional information is required.

---

# 12. Full Model

## 12.1 Purpose

The Full Model mode allows the user to calculate the complete model without relying on the limiting approximation used in Quick Fit.

The specification intentionally does not prescribe the mathematical or numerical implementation.

## 12.2 Entry routes

The user should be able to enter the Full Model in two ways:

### From experimental data
Use the dataset already imported in Your Particle.

### Without experimental data
Provide physical/model parameters directly and calculate a predicted curve.

## 12.3 Starting from Quick Fit

When entering from Quick Fit:

- imported data should remain loaded;
- parameters inferred or selected in Quick Fit should carry forward where meaningful;
- the limiting fit should remain available for comparison.

## 12.4 Full-model plot

The user should be able to view:

- experimental points, if present;
- Quick Fit curve, if present;
- Full Model curve.

The graph should allow individual curves to be hidden/shown.

## 12.5 Difference assessment

The interface should help the user assess whether the limiting approximation differs materially from the Full Model.

Possible outputs include:

- visual overlay;
- residual comparison;
- numerical difference metric;
- difference in characteristic degradation times.

The exact metric may be determined later.

## 12.6 Manual parameter exploration

The user should be able to modify selected physical parameters and recalculate the model.

Examples of categories:

- particle geometry;
- particle dimensions;
- porosity;
- material/treatment descriptors;
- environmental parameters;
- coating/barrier parameters;
- transport-related parameters;
- dissolution-related parameters.

The final list will follow the scientific model.

## 12.7 Fixed/free parameter concept

The interface should distinguish between:

- fixed parameters;
- manually varied parameters;
- parameters selected for fitting.

## 12.8 One-parameter fitting

A practical fitting mode should allow the user to:

1. fix all required parameters except one;
2. choose one parameter to fit;
3. fit that parameter to the experimental degradation curve;
4. display the resulting curve and fitted parameter.

This should be presented as a scientifically controlled alternative to unconstrained multi-parameter fitting.

## 12.9 Effective-parameter fitting

Where scientifically appropriate, the user may instead fit an effective aggregate parameter or characteristic timescale while keeping the rest of the model fixed.

## 12.10 Multi-parameter fitting

Fully automatic fitting of many physical parameters simultaneously is not required for the early product and should not be presented as reliable unless identifiability has been established.

A later version may expose carefully constrained multi-parameter fitting.

## 12.11 Recalculation UX

Changing a parameter should make it clear that the displayed prediction is now based on a modified assumption.

The interface should distinguish:

- current parameter values;
- original values;
- fitted values;
- modified exploratory values.

## 12.12 Comparison against experiment

When experimental data are present, the Full Model view should provide:

- curve overlay;
- residuals or equivalent fit-quality view;
- goodness-of-fit information;
- visible list of parameter values used.

---

# 13. Export from Your Particle

## 13.1 Purpose

A user should be able to save the scientific result of an analysis rather than only take a screenshot.

## 13.2 Minimum export contents

Export should be capable of including:

- original experimental points;
- processed/normalised points if applicable;
- point inclusion/exclusion state;
- Quick Fit predicted curve;
- Full Model predicted curve;
- time coordinates for calculated curves;
- fixed parameters;
- fitted parameters;
- inferred parameters;
- units;
- selected observable;
- selected model mode;
- fitting settings;
- weighting setting;
- fit metrics;
- analysis timestamp/version information where useful.

## 13.3 Export formats

The first implementation may support CSV / delimited text.

Later versions may additionally support:

- spreadsheet workbook;
- structured JSON;
- publication-ready figure export;
- compact analysis report.

The final format set should be decided separately.

---

# 14. Design Your Nanoparticle / Sandbox

## 14.1 Purpose

This section is a forward-design and virtual-experiment workspace.

It is for users who do not necessarily have experimental degradation data and want to ask:

> What degradation behaviour would I expect if I made a particle with these properties?

and eventually:

> What particle properties could give me approximately the degradation time I want?

## 14.2 Starting modes

The user should be able to start in at least two ways:

### Blank design
Begin with a fresh parameter set.

### Start from literature example
Load the available parameters from an Example and modify them.

A later version may also allow loading a previously exported user analysis/design.

## 14.3 Input categories

The design form should expose scientifically relevant categories such as:

### Particle
- material;
- particle geometry;
- particle size;
- porosity;
- pore geometry / morphology where represented.

### Material treatment
- oxidation-related descriptors;
- calcination-related descriptors;
- other material-processing variables represented by the final model.

### Environment
- temperature;
- pH;
- solution conditions;
- particle concentration where relevant;
- other experimental conditions.

### Surface / barrier layer
- presence/absence of coating;
- coating descriptors required by the model.

### Model assumptions
- applicable model regime/settings;
- known vs assumed parameters.

The exact scientific parameter list will be maintained separately from this functional specification.

## 14.4 Forward virtual experiment

After the user enters parameters, the site should calculate and show:

- predicted degradation curve;
- characteristic timescale(s);
- time to selected dissolution/degradation thresholds.

## 14.5 Standard degradation metrics

At minimum, the Sandbox should calculate:

- **t50**: time to 50% degradation/dissolution;
- **t90**: time to 90% degradation/dissolution.

If the observable is remaining material, the wording/definition should be displayed unambiguously.

Additional thresholds may be configurable later.

## 14.6 Real-time exploration

The user should be able to change one or more parameters and quickly rerun the virtual experiment.

The UI should make it easy to compare:

- previous state;
- current state;
- optionally a small set of saved variants.

## 14.7 Save design variant

The user should be able to save a temporary design configuration within the current session, assign it a label, and compare it against another configuration.

This is useful for questions such as:

- uncoated vs coated;
- lower vs higher oxidation;
- smaller vs larger particle;
- different environmental conditions.

## 14.8 Target-driven design

A later high-value mode should allow the user to specify a desired outcome such as:

- t50 ≈ 7 days;
- t90 within a target window;
- degradation remaining above/below a target at a chosen time.

The system should then help identify parameter combinations compatible with the target.

## 14.9 Target design output

The result should not imply that there is necessarily one unique design.

Where multiple solutions exist, the user may be shown:

- candidate parameter sets;
- feasible ranges;
- trade-offs;
- sensitivity to selected parameters.

## 14.10 Parameter constraints

The user should be able to constrain parameters before target search, for example:

- particle size must remain within a practical range;
- a treatment condition is fixed;
- coating is mandatory;
- pH is dictated by the biological environment.

## 14.11 Evidence behind parameters

For every empirically supported factor, the user should be able to inspect which Examples support the dependency.

This may appear as:

- evidence icon;
- supporting-data drawer;
- link to filtered Examples.

## 14.12 Extrapolation warnings

If the user selects a parameter outside the range supported by the underlying examples, the site should warn that the prediction is extrapolative.

The model may still calculate a result if scientifically permitted, but the confidence distinction must be visible.

## 14.13 Factor interaction warning

Where the current model treats effects independently or approximately but interactions may exist, the site should say so.

For example, combining two stabilising modifications should not automatically be presented as experimentally validated unless corresponding evidence exists.

## 14.14 Sandbox export

The user should be able to export:

- chosen design parameters;
- predicted curve;
- t50 / t90;
- characteristic time(s);
- model assumptions;
- evidence/source references where appropriate.

---

# 15. Cross-section integration

The site should feel like one connected scientific environment rather than five unrelated pages.

## 15.1 Examples → Your Particle

Where possible, an Example can be loaded as a predefined dataset into the analysis workflow.

## 15.2 Examples → Sandbox

An Example can serve as a starting particle/environment configuration.

## 15.3 Your Particle → Sandbox

A user who has fitted their own particle should eventually be able to use the resulting parameter set as a starting point for design exploration.

## 15.4 Sandbox → Examples

Evidence links should open relevant example datasets.

## 15.5 Theory → Tools

Theory should link to practical demonstrations of each model regime.

## 15.6 Tools → Theory

Complex controls should include contextual help that can open the relevant Theory explanation.

---

# 16. Scientific graph requirements

All scientific plots should use a consistent interaction model.

## 16.1 Required capabilities

- axes with units;
- clearly distinguishable experimental points and model curves;
- interactive legend;
- show/hide curves;
- hover values;
- zoom;
- reset view;
- readable state on both light and dark UI if both are supported.

## 16.2 Experimental points

Experimental data should never be visually confused with model predictions.

## 16.3 Residual plots

Residuals should be available where fitting quality is important, especially in Your Particle.

They need not be shown by default.

## 16.4 Characteristic markers

Where helpful, the graph may show visual markers for values such as:

- t50;
- t90;
- other selected thresholds.

## 16.5 Data table

For scientific transparency, plotted data should be inspectable in tabular form when practical.

---

# 17. Data model requirements at product level

This section describes required information categories, not implementation schemas.

## 17.1 Literature Example entity

Each example should be capable of storing:

- unique identifier;
- display title;
- short description;
- source citation;
- source link;
- source figure/table;
- experimental data series;
- units;
- sample metadata;
- environmental metadata;
- measurement metadata;
- treatment metadata;
- model curves;
- model parameter metadata;
- tags / filter categories;
- notes;
- provenance / digitisation information.

## 17.2 User dataset entity

A user dataset should retain:

- original uploaded data;
- parsed data;
- column mapping;
- units;
- observable type;
- exclusions;
- transformations;
- fit results;
- full-model runs;
- parameter states;
- export metadata.

## 17.3 Particle configuration entity

A particle configuration should retain:

- all relevant model input parameters;
- source of each parameter;
- units;
- whether each parameter is fixed / fitted / assumed;
- associated prediction;
- characteristic metrics;
- model version / assumptions.

This configuration should be reusable between relevant site sections.

---

# 18. User-facing scientific provenance

## 18.1 Literature provenance

Literature-derived data should identify:

- article;
- figure/table if known;
- whether values were reported directly or digitised;
- any transformation made before use.

## 18.2 Fit provenance

Any fit shown to the user should identify:

- dataset used;
- model mode;
- free parameters;
- fixed parameters;
- weighting;
- exclusions;
- fit quality.

## 18.3 Prediction provenance

Any sandbox prediction should identify:

- parameter values;
- source/assumption status;
- evidence range where available;
- whether prediction involves extrapolation.

---

# 19. Accessibility and usability

## 19.1 Avoid colour-only meaning

Curves and statuses should not rely solely on colour differences.

Use combinations of:

- line style;
- symbols;
- labels;
- toggles.

## 19.2 Tooltips

Scientific parameters may have concise tooltips explaining:

- meaning;
- unit;
- whether a larger value generally increases or decreases degradation time, if established.

Tooltips should not replace the Theory section.

## 19.3 Advanced settings

Advanced scientific controls should be collapsed by default so that a first-time user is not overwhelmed.

## 19.4 Error recovery

A failed fit or invalid model run should not destroy the current data/parameter configuration.

The user should be told:

- what failed;
- which inputs may need attention;
- whether they can continue by adjusting parameters.

---

# 20. Non-goals for initial versions

The following are explicitly not required in the early MVPs:

- cross-example comparison;
- automatic fitting of many physical parameters simultaneously;
- complete Theory content;
- publication-quality automatic report generation;
- user accounts;
- cloud project storage;
- collaboration features;
- database editing UI for literature curators;
- fully automated extraction of data from papers;
- exhaustive support for arbitrary experimental file formats;
- mobile-first fitting workflow;
- automatic claim that a target nanoparticle design is experimentally validated.

These may be revisited later.

---

# 21. Development roadmap

The project should be implemented incrementally so that every stage produces a usable, inspectable website.

The roadmap below deliberately separates functional milestones from the choice of implementation technology.

---

# Phase 0 — Clickable layout / site shell

## Goal

Create a visually coherent site that can be navigated and reviewed before any scientific engine is implemented.

## Required functionality

- global site layout;
- final five main navigation entries:
  - Home;
  - Theory;
  - Examples;
  - Your Particle;
  - Design Your Nanoparticle;
- responsive header/navigation;
- basic visual system;
- placeholder content for all pages;
- representative empty graph areas / cards / forms;
- no real fitting or model calculation required.

## Home

Implement the real structure of the Home page sufficiently to judge the overall presentation.

## Theory

Placeholder only.

It should exist in the correct navigation position but may contain a short “Theory content will be added later” block plus representative layout.

## Examples

Create catalogue and detail-page mockups using temporary/mock data if necessary.

## Your Particle

Show static or non-functional placeholders for:

- upload area;
- data preview;
- Quick Fit;
- Full Model;
- export.

## Sandbox

Show static/non-functional parameter controls and result graph placeholders.

## Acceptance criteria

- user can navigate to every final section;
- layout feels like one coherent product;
- page hierarchy is understandable;
- no scientific computation is required;
- design can be reviewed before deeper implementation.

---

# Phase 1 — Examples MVP

## Goal

Make the literature Examples section the first genuinely functional scientific part of the site.

This is expected to be the easiest high-value feature because curated JSON datasets already exist or will be prepared.

## Required functionality

### Catalogue
- load examples from structured data;
- display example cards/list;
- search;
- basic filtering if metadata are already sufficiently standardised;
- open an example.

### Example detail
- title;
- description;
- article citation/link;
- experimental metadata;
- experimental points;
- predefined model curve(s) if already contained in the source data;
- interactive plot;
- curve visibility toggles;
- zoom/reset;
- inspect data values.

### Data robustness
- tolerate optional/missing metadata;
- do not show broken empty fields;
- distinguish unavailable information from zero/false values.

## Explicitly excluded from Phase 1

- compare examples;
- loading into Your Particle;
- advanced cross-dataset analytics;
- automatic fitting;
- full-model calculation.

## Acceptance criteria

A user can browse real scientific examples, open any supported example, understand what was measured, see the data and associated curves, and follow the link to the source article.

---

# Phase 1.1 — Examples metadata hardening

## Goal

Standardise the Examples dataset enough that it can support the later calculator, evidence system, and sandbox.

## Required work at product level

Ensure example records can represent:

- scientific question;
- sample identity;
- morphology;
- relevant material parameters;
- experimental environment;
- treatment;
- measured observable;
- units;
- publication provenance;
- model outputs;
- factor tags.

## Acceptance criteria

Examples can be reliably searched/filtered and can later act as evidence sources for parameter dependencies.

---

# Phase 2 — Your Particle: import + Quick Fit

## Goal

Allow an experimental researcher to upload their own degradation curve and fit it with a simple limiting model.

## Required functionality

### Import
- CSV / ASCII upload;
- delimiter selection;
- header-line control;
- column mapping;
- preview;
- observable selection;
- units;
- validation.

### Data inspection
- table;
- initial graph;
- include/exclude individual points.

### Quick Fit
- select supported simplified model mode;
- run fit;
- display fitted curve;
- display effective fitted parameter(s);
- display characteristic time where applicable;
- basic goodness-of-fit information;
- selectable fitting-weight mode;
- clear fixed/free parameter display.

### Interpretation
- explain that fitted effective quantities may combine multiple physical factors;
- do not imply unique microscopic parameter recovery where it is not possible.

### Export
- export experimental points;
- fitted curve;
- fitted parameters;
- units;
- fitting settings.

## Explicitly excluded from Phase 2

- complete-model numerical solution;
- broad parameter optimisation;
- target-driven particle design;
- literature comparison mode.

## Acceptance criteria

A user can take a normal laboratory text/CSV degradation dataset, import it without manually reformatting it into a rigid site-specific file, fit a supported simple model, understand the fitted timescale, and export the result.

---

# Phase 2.1 — Effective parameter calculator

## Goal

Turn the Quick Fit result into a more useful physical interpretation tool.

## Required functionality

- use the fitted effective timescale/rate;
- display model-relevant physical factors;
- allow user to enter known values;
- mark unknown values;
- calculate compatible unknown quantity/range where the model allows;
- show non-identifiability when no unique answer exists;
- link empirical factor relationships to supporting Examples.

## Acceptance criteria

A user can combine their fitted effective result with independent knowledge of their experiment to obtain a physically meaningful estimate or constraint rather than only a curve fit.

---

# Phase 3 — Full Model

## Goal

Allow the user to solve and inspect the complete coupled model and compare it with the limiting approximation.

## Required functionality

### From Quick Fit
- retain uploaded data;
- retain Quick Fit result;
- transfer relevant parameter values.

### Standalone full-model run
- allow user to enter a complete parameter set without uploading data;
- calculate a full-model degradation curve.

### Comparison
- show experimental points;
- show limiting fit;
- show Full Model;
- allow curves to be toggled;
- provide a meaningful comparison of the limiting and full calculations.

### Parameter exploration
- edit physical/model parameters;
- rerun calculation;
- preserve original values for comparison where useful.

### One-parameter inverse mode
- fix all parameters except one;
- choose one parameter to fit;
- fit it against experimental data;
- report fitted value and fit quality.

### Effective-parameter fit
- where supported, allow an effective aggregate parameter to be fitted within the Full Model.

### Export
- full-model curve;
- all parameter values/statuses;
- experimental data;
- fit/comparison metrics;
- settings.

## Explicitly excluded from Phase 3 core

- unconstrained many-parameter inverse fitting;
- automated global nanoparticle design;
- cross-example compare.

## Acceptance criteria

A user can determine whether the simple limiting fit is adequate for their dataset and can explore how physically plausible parameter changes affect the complete-model prediction.

---

# Phase 3.1 — Scientific workflow polish

## Goal

Make the Full Model practical rather than merely technically available.

## Potential functionality

- residual panel;
- parameter sensitivity indicators;
- saved parameter variants;
- clearer warnings about underdetermined fits;
- quick revert to Quick Fit parameter set;
- compare current vs previous full-model run.

This phase should be driven by actual use during testing.

---

# Phase 4 — Design Your Nanoparticle / Sandbox

## Goal

Enable forward virtual experiments for hypothetical particles.

## Required functionality

### Start blank
- enter particle and environment parameters.

### Start from Example
- load available example metadata into the design form.

### Run virtual experiment
- calculate predicted degradation curve;
- calculate characteristic time(s);
- calculate t50;
- calculate t90.

### Explore
- modify parameters;
- recalculate;
- inspect effects;
- save a few named design variants within the session.

### Evidence
- show where factor dependencies are supported by Examples;
- warn about extrapolation beyond evidence ranges.

### Export
- parameter set;
- predicted curve;
- characteristic metrics;
- assumptions.

## Acceptance criteria

A user can create a hypothetical particle configuration and obtain a reproducible model-based prediction of its degradation profile.

---

# Phase 4.1 — Target-driven design

## Goal

Allow the user to work backwards from a desired degradation outcome.

## Required functionality

The user can specify a target such as:

- desired t50;
- desired t90;
- target degradation fraction at a chosen time.

The user can also specify constraints such as:

- fixed environment;
- allowed particle-size range;
- mandatory coating;
- fixed treatment.

The site returns scientifically compatible candidate parameter combinations or ranges rather than pretending there is necessarily a single unique solution.

## Required presentation

- candidate designs;
- target achieved / deviation from target;
- key trade-offs;
- evidence/extrapolation indicators;
- predicted curves for selected candidates.

## Acceptance criteria

The Sandbox can be used for preliminary experiment planning rather than only manual slider exploration.

---

# Phase 5 — Theory

## Goal

Complete the educational/scientific explanation after the practical workflows and terminology have stabilised.

## Required functionality

Implement the full Theory specification described earlier, including:

- physical picture;
- effective porosity representation;
- general transport/source model;
- symmetry reduction;
- limiting regimes;
- general coupled regime;
- surface-area dependence;
- supported pore geometries;
- coatings;
- links into live Examples and tools.

## Why implemented late

The final Theory should use:

- the same terminology as the working application;
- the same parameter names;
- the same graphical conventions;
- real examples already available in the site.

This avoids writing a theoretical section that later diverges from the implemented product.

## Acceptance criteria

A reader can move from the Theory section directly into concrete Examples or model tools and see the same concepts represented consistently.

---

# Phase 6 — Post-MVP enhancements / “ribbons”

These features are desirable but should not block the core scientific tool.

## 6.1 Compare Examples

- select multiple literature examples;
- overlay curves;
- side-by-side comparison;
- compare metadata.

## 6.2 Example-to-example normalisation tools

Where scientifically appropriate, allow datasets to be compared on normalised axes.

## 6.3 Rich exports

- Excel workbook;
- structured JSON;
- figure image export;
- compact PDF/HTML scientific report.

## 6.4 Saved projects

Optional persistent user workspaces if later required.

## 6.5 Shareable configurations

Generate a reproducible configuration that another researcher can open.

## 6.6 Additional observables

Add more experimental measurement types when scientifically justified.

## 6.7 Additional geometries / material classes

Extend the model/tooling to cases supported by future work.

## 6.8 Sensitivity analysis

Provide systematic parameter-sensitivity exploration.

## 6.9 Uncertainty propagation

Propagate known uncertainty in inputs to uncertainty in predicted degradation.

## 6.10 Publication figure reproduction

Allow selected site plots to reproduce specific paper figures interactively.

---

# 22. Proposed user workflows

## Workflow A — Reader exploring the paper

1. Open Home.
2. Read one-paragraph explanation.
3. Open Examples.
4. Select a literature dataset.
5. Inspect experimental points and model curve.
6. Open the publication source.
7. Optionally open Theory for explanation of the model regime.

## Workflow B — Experimentalist with degradation data

1. Open Your Particle.
2. Upload CSV/ASCII.
3. Configure parsing.
4. Map time and measurement columns.
5. Select observable.
6. Inspect parsed graph.
7. Run Quick Fit.
8. Inspect fitted timescale and goodness of fit.
9. Export if sufficient.
10. Otherwise open Full Model.
11. Compare full calculation to limiting fit.
12. Adjust or fit a selected uncertain parameter.
13. Export final analysis.

## Workflow C — Researcher investigating an uncertain particle property

1. Load own data.
2. Run Quick Fit.
3. Enter Full Model.
4. Fix trusted measured parameters.
5. Select one uncertain quantity.
6. Fit or manually explore that quantity.
7. Inspect whether the result is physically plausible.
8. Check supporting literature examples.
9. Export result and assumptions.

## Workflow D — Designing a hypothetical particle

1. Open Design Your Nanoparticle.
2. Start blank.
3. Enter desired experimental environment.
4. Enter initial particle parameters.
5. Run virtual experiment.
6. Inspect degradation curve, t50, t90.
7. Modify particle design.
8. Save variants.
9. Compare predicted behaviour.
10. Export preferred design.

## Workflow E — Starting design from literature

1. Open Examples.
2. Choose a relevant published particle.
3. Click Load into Design Sandbox.
4. Modify one or more parameters.
5. Compare prediction with the original example.
6. Inspect whether the modified values are within supported evidence ranges.
7. Export design.

## Workflow F — Target degradation time

1. Open Design Sandbox.
2. Select target-driven mode.
3. Enter desired t50/t90 or degradation fraction at time T.
4. Fix unavoidable experimental conditions.
5. Define allowed ranges for design parameters.
6. Run target search.
7. Inspect compatible candidate designs.
8. Compare candidates.
9. Review evidence/extrapolation.
10. Export selected candidate(s).

---

# 23. MVP priority summary

## MVP 0 — Shell
**Deliverable:** clickable final site layout with placeholders.

## MVP 1 — Examples
**Deliverable:** real literature dataset browser + interactive individual example plots.

## MVP 2 — Quick Fit
**Deliverable:** upload own data + simple limiting-model fit + export.

## MVP 2.1 — Parameter calculator
**Deliverable:** interpret fitted effective timescale using known physical parameters and literature-backed factor relationships.

## MVP 3 — Full Model
**Deliverable:** full calculation, comparison against Quick Fit, manual parameter exploration, controlled one-parameter fitting.

## MVP 4 — Design Sandbox
**Deliverable:** choose particle/environment parameters → predicted curve + t50/t90 + export.

## MVP 4.1 — Target Design
**Deliverable:** target degradation behaviour → compatible parameter combinations.

## MVP 5 — Theory
**Deliverable:** complete interactive theoretical explanation linked to the working tools.

## Post-MVP
**Deliverable:** comparisons, richer exports, saved projects, uncertainty/sensitivity tools, and other non-essential enhancements.

---

# 24. Definition of the first genuinely useful release

The first release that can be considered scientifically useful rather than merely demonstrative should include:

- functioning Home/navigation;
- functioning Examples browser;
- real experimental datasets;
- interactive plots;
- working Your Particle importer;
- Quick Fit;
- characteristic fitted parameter/timescale output;
- export of the fit result.

This corresponds approximately to completion of **Phase 2**.

---

# 25. Definition of the core complete scientific product

The core product can be considered functionally complete when it includes:

- Home;
- Examples;
- Your Particle Quick Fit;
- effective-parameter interpretation;
- Full Model;
- parameter exploration / one-parameter fitting;
- Design Sandbox;
- t50/t90 prediction;
- evidence links;
- exports;
- final Theory.

Cross-example comparison and other embellishments are not required for this milestone.

---

# 26. Open scientific/product decisions to resolve later

The following items should remain open until the relevant scientific work is finalised:

1. exact parameter names and symbols;
2. exact analytical forms used in each limiting regime;
3. exact full-model mathematical formulation used by the production site;
4. final pore-geometry formulae;
5. final coating formulation;
6. exact fitting-weight options;
7. which fit-quality metrics are scientifically preferred;
8. exact dependencies of characteristic times/rates on experimental factors;
9. which factors can legitimately be treated independently;
10. valid parameter ranges for each empirical dependency;
11. rules for extrapolation;
12. which quantities can be uniquely inferred from one degradation curve;
13. final observable conversions between dissolved Si, remaining Si, and silicic-acid concentration;
14. final list of supported units;
15. final export formats;
16. exact terminology for the last section:
    - Design Your Nanoparticle;
    - Nanoparticle Sandbox;
    - Bake Your Own Nanoparticle;
    - another final public-facing name.

These decisions should be documented separately from this functional specification so that implementation requirements remain stable even while the scientific model is refined.

---

# 27. Product success criterion

A successful implementation should allow a researcher to move from published evidence or their own experimental degradation curve to a scientifically interpretable model result without writing code.

At the most advanced level, the same environment should allow them to explore a hypothetical particle design and ask:

> **“Given the material properties and experimental conditions I can control, what degradation profile should I expect, and what should I change if I need a different timescale?”**

That is the central practical goal of the website.
