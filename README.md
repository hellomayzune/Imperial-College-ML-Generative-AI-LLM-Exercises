# Generative AI & Large Language Model Learning Notebooks

A collection of practical Jupyter notebooks exploring **Generative AI,
Large Language Models (LLMs), multimodal AI, optimisation, and
AI-assisted building engineering workflows**.

These notebooks form part of my learning journey through the **Imperial
College London Professional Certificate in Machine Learning / AI**. Many
of the exercises are adapted or developed from examples and ideas found
online and are intended primarily for **learning, experimentation, and
prototyping**.

> **Important:** The notebooks are educational demonstrations. Several
> components intentionally simulate production systems, including LLM
> calls, BIM integrations, vector databases, building-performance
> models, and BACnet hardware interfaces. Results should not be treated
> as engineering, regulatory, or operational advice without appropriate
> professional validation.

------------------------------------------------------------------------

## Notebook Collection

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Notebook                                                                                                                                                                                                                   Main theme              Key concepts
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------------- -----------------------
  [`Generative BIM Carbon Optimisation.ipynb`](./Generative%20BIM%20Carbon%20Optimisation.ipynb)                                                                                                                             Generative BIM + carbon Embodied carbon,
                                                                                                                                                                                                                                                     operational carbon, EPD
                                                                                                                                                                                                                                                     factors, parametric
                                                                                                                                                                                                                                                     design, Pareto
                                                                                                                                                                                                                                                     optimisation

  [`Generative BIM Cost Optimisation.ipynb`](./Generative%20BIM%20Cost%20Optimisation.ipynb)                                                                                                                                 Generative BIM +        Parametric BIM data,
                                                                                                                                                                                                                             structural cost         structural checks,
                                                                                                                                                                                                                                                     quantity take-off,
                                                                                                                                                                                                                                                     differential evolution,
                                                                                                                                                                                                                                                     penalty functions

  [`Generative BIM Massing and Microclimate AI Optimizer.ipynb`](./Generative%20BIM%20Massing%20and%20Microclimate%20AI%20Optimizer.ipynb)                                                                                   AI-assisted building    PyTorch surrogate
                                                                                                                                                                                                                             massing                 modelling, wind-risk
                                                                                                                                                                                                                                                     prediction, NSGA-II,
                                                                                                                                                                                                                                                     Pareto fronts, BIM
                                                                                                                                                                                                                                                     geometry

  [`LLM and AI Compliance in Honolulu DPP.ipynb`](./LLM%20and%20AI%20Compliance%20in%20Honolulu%20DPP.ipynb)                                                                                                                 AI-assisted plan        Multimodal extraction,
                                                                                                                                                                                                                             checking                deterministic rules,
                                                                                                                                                                                                                                                     zoning/building-code
                                                                                                                                                                                                                                                     checks, cited reports

  [`LLM-Driven Structured Parsing of Thermal Complaints into PMV and BACnet Setpoint Deltas.ipynb`](./LLM-Driven%20Structured%20Parsing%20of%20Thermal%20Complaints%20into%20PMV%20and%20BACnet%20Setpoint%20Deltas.ipynb)   LLM + building controls Structured outputs,
                                                                                                                                                                                                                                                     Pydantic, PMV, ASHRAE
                                                                                                                                                                                                                                                     55, BACnet control
                                                                                                                                                                                                                                                     deltas

  [`LLM-Driven VLM–RAG Integration for Building Management System Control.ipynb`](./LLM-Driven%20VLM%E2%80%93RAG%20Integration%20for%20Building%20Management%20System%20Control.ipynb)                                       Multimodal AI + BMS     VLMs, RAG, SDS
                                                                                                                                                                                                                                                     retrieval, HVAC
                                                                                                                                                                                                                                                     constraints, IEQ,
                                                                                                                                                                                                                                                     BACnet orchestration

  [`LLM-Enhanced Model Predictive Control.ipynb`](./LLM-Enhanced%20Model%20Predictive%20Control.ipynb)                                                                                                                       LLM + MPC               Natural-language
                                                                                                                                                                                                                                                     intent, structured
                                                                                                                                                                                                                                                     constraints, thermal RC
                                                                                                                                                                                                                                                     models, optimisation,
                                                                                                                                                                                                                                                     energy tariffs
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 1. Generative BIM Carbon Optimisation

**Focus:** Exploring how generative design can balance **embodied
carbon** and **operational carbon** across alternative building
configurations.

The notebook creates a parametric search space of approximately **1,000
design variations**, varying:

-   Number of floors
-   Floor area
-   South-facing window-to-wall ratio (WWR)
-   Shading depth
-   Structural material choice, including concrete and mass timber

It then estimates:

1.  Material quantities and embodied carbon using simplified EPD-style
    carbon factors.
2.  Operational energy/carbon using heuristic relationships between
    glazing, shading, thermal mass, and EUI.
3.  The **Pareto frontier** between embodied and operational carbon.

**Key learning:** Multi-objective design is not necessarily about
finding one universally "best" solution. Pareto-optimal solutions expose
the trade-offs between competing objectives.

------------------------------------------------------------------------

## 2. Generative BIM Cost Optimisation

**Focus:** Using evolutionary optimisation to explore structural beam
dimensions while considering both **cost and structural safety**.

The notebook demonstrates:

-   Parametric beam dimensions (`b` and `d`)
-   Material metadata such as cost, density, and yield strength
-   Quantity/cost calculations
-   Bending stress and deflection checks
-   `scipy.optimize.differential_evolution`
-   Penalty functions for unsafe designs
-   Visualisation of the cost/design space

The optimisation searches beam width and depth within defined ranges and
penalises candidates that violate structural limits such as stress or
the **L/360 deflection criterion**.

**Key learning:** Generative optimisation can explore a much larger
design space than manually selecting a small number of predefined
options, while engineering constraints can be incorporated directly into
the objective evaluation.

------------------------------------------------------------------------

## 3. Generative BIM Massing & Microclimate AI Optimizer

**Focus:** Combining a neural-network surrogate model with a
**multi-objective evolutionary algorithm** for early-stage building
massing.

The building is represented by three principal parameters:

-   Height
-   Rotation angle
-   Facade porosity

A PyTorch neural network acts as a simplified **physics surrogate**,
producing a 10 × 10 wind-speed field. The optimisation then uses **DEAP
/ NSGA-II** to:

-   Maximise gross floor area
-   Minimise the number of high-wind-risk cells
-   Explore alternative building geometries
-   Identify non-dominated solutions

The notebook also discusses how the simplified parameterisation could be
extended to real BIM geometry using formats and tools such as **IFC,
OBJ, STL, Revit, Rhino/Grasshopper, and Blender/FreeCAD**.

**Key learning:** A surrogate model can make repeated optimisation
evaluations cheaper, while evolutionary algorithms can search for useful
trade-offs between competing architectural and environmental objectives.

------------------------------------------------------------------------

## 4. LLM and AI Compliance in Honolulu DPP

**Focus:** Demonstrating an AI-assisted workflow for preliminary
architectural plan compliance checking.

The notebook separates the process into four stages:

1.  **Rule ingestion** --- converting regulatory text into
    machine-readable constraints.
2.  **Plan data extraction** --- representing CAD/BIM-derived dimensions
    and properties.
3.  **Deterministic verification** --- performing the actual
    numerical/spatial checks.
4.  **LLM citation/report generation** --- presenting the results in a
    reviewer-friendly format.

The example considers zoning and building-code checks such as:

-   Rear-yard setback
-   Building height
-   Bedroom egress window dimensions/area
-   Other plan-review requirements represented in the example

A central design principle is that the **deterministic verification
engine performs the compliance calculations**, while the LLM is used to
help interpret information and generate a readable, cited report.

**Key learning:** LLMs can support regulatory workflows, but
deterministic rules and human review remain important when the result
has legal or compliance consequences.

------------------------------------------------------------------------

## 5. LLM-Driven Structured Parsing of Thermal Complaints into PMV and BACnet Setpoint Deltas

**Focus:** Turning natural-language occupant feedback into structured
building-control information.

Example input:

> "Students near the windows in Room 102 are shivering during their
> test, but the middle of the room feels really stuffy and heavy."

The notebook demonstrates a pipeline that:

1.  Extracts thermal and air-quality perceptions.
2.  Anchors the complaint to a spatial zone.
3.  Maps contextual information to PMV-related variables.
4.  Uses **Pydantic schemas** and enumerations to constrain structured
    LLM output.
5.  Produces multiple HVAC control deltas rather than only changing a
    global thermostat.
6.  Passes the resulting commands through a simulated BACnet adapter.

The structured output includes concepts such as:

-   Thermal sensation
-   Air-quality perception
-   Metabolic rate
-   Clothing insulation
-   Estimated PMV
-   Temperature setpoint adjustment
-   Outdoor-air damper adjustment
-   Reheat adjustment
-   Fan-speed adjustment

**Key learning:** Structured outputs can provide a bridge between
flexible natural-language interfaces and systems that require
predictable, typed parameters.

------------------------------------------------------------------------

## 6. LLM-Driven VLM--RAG Integration for Building Management System Control

**Focus:** Combining **vision-language models, retrieval-augmented
generation, and building controls**.

The demonstrated architecture is:

``` text
Camera / Visual Frame
        │
        ▼
Vision-Language Model
        │
        ▼
Structured Visual Observations
        │
        ▼
RAG Knowledge Retrieval
 ┌──────┴─────────────┐
 │                    │
SDS / hazards     HVAC capabilities
 │                    │
 └────────┬───────────┘
          ▼
    LLM Decision Agent
          │
          ▼
    BACnet Command
          │
          ▼
   Building Control
```

The example uses visual observations of cleaning equipment/chemicals
alongside:

-   TVOC
-   CO₂
-   PM2.5
-   Safety Data Sheet guidance
-   HVAC equipment capabilities

The decision agent synthesises this context and generates a structured
BACnet control action, such as adjusting outdoor-air and recirculation
dampers, fan speed, or a carbon scrubber.

The notebook also includes a more detailed multi-zone architecture using
**BAC0**.

**Key learning:** RAG can provide domain-specific context to an LLM,
while a VLM can connect visual observations to that context. The
important architectural idea is the separation between perception,
retrieval, decision-making, and hardware execution.

------------------------------------------------------------------------

## 7. LLM-Enhanced Model Predictive Control (MPC)

**Focus:** Using an LLM as a semantic interface to a conventional
**physics-based MPC optimiser**.

The notebook separates the workflow into:

``` text
Natural-language operational intent
              │
              ▼
       LLM semantic parser
              │
              ▼
   Structured MPC constraints
              │
              ▼
 Physics-based thermal RC model
              │
              ▼
      Optimisation solver
              │
              ▼
        HVAC strategy
              │
              ▼
     LLM explanation/audit
```

The example considers an executive meeting in Zone 3 and translates the
operational instruction into dynamic temperature constraints.

The MPC then uses:

-   A simplified resistance-capacitance (RC) thermal model
-   Ambient-temperature forecasts
-   Internal heat gains
-   Electricity prices
-   Temperature constraints
-   Pre-cooling permission

The example illustrates **pre-cooling before a high-price tariff
period**, allowing the building to meet comfort requirements during the
meeting while reducing cooling demand during more expensive hours.

**Key learning:** The LLM does not need to replace the optimiser. It can
instead act as a semantic translation layer that converts human intent
into structured constraints, while the physics-based optimisation
remains responsible for calculating the control strategy.

------------------------------------------------------------------------

## Common Themes Across the Notebooks

These exercises explore several recurring patterns in applied Generative
AI:

### 1. Natural language → structured parameters

LLMs are particularly useful when human instructions need to become
machine-readable parameters:

``` text
Human intent
    ↓
LLM
    ↓
Structured schema
    ↓
Conventional software / optimiser / controller
```

### 2. AI + deterministic computation

Several notebooks deliberately separate probabilistic AI components from
deterministic calculations.

Examples include:

-   LLM → MPC constraints → numerical optimiser
-   LLM → compliance interpretation → deterministic rule engine
-   LLM → PMV/control parameters → HVAC interface
-   VLM → observations → RAG → control decision

This separation is useful when numerical accuracy, traceability, and
predictable behaviour matter.

### 3. Generative optimisation

The BIM notebooks demonstrate how AI/optimisation can explore large
design spaces rather than evaluating only a few manually selected
alternatives.

The optimisation objectives include:

-   Carbon
-   Cost
-   Floor area
-   Wind risk
-   Structural safety

### 4. Multi-objective optimisation and Pareto fronts

The carbon and massing notebooks show the idea of **Pareto optimality**:
improving one objective may require accepting a deterioration in
another.

Rather than producing a single answer, the algorithm can expose a set of
non-dominated alternatives for designers to evaluate.

### 5. Multimodal AI

The BMS and compliance examples move beyond text-only LLMs by combining:

-   Visual information
-   Structured sensor data
-   Regulatory/domain knowledge
-   Natural language
-   Building-system metadata

### 6. AI as an orchestration layer

A recurring architectural pattern is:

``` text
AI / LLM
   ↓
Interpretation & orchestration
   ↓
Specialised deterministic tools
   ↓
Engineering / optimisation / control result
```

This is particularly relevant to AEC, building performance, and
smart-building applications where an LLM alone should not be responsible
for the final engineering calculation.

------------------------------------------------------------------------

## Learning Objectives

Working through these notebooks provides practical exposure to:

-   Generative AI and LLM application patterns
-   Structured LLM outputs
-   Pydantic schema validation
-   Prompt-based semantic parsing
-   Vision-language model concepts
-   Retrieval-augmented generation (RAG)
-   Parametric and generative design
-   Evolutionary algorithms
-   NSGA-II and Pareto optimisation
-   Surrogate modelling with PyTorch
-   Building thermal modelling
-   Model Predictive Control
-   Building automation concepts
-   BACnet-oriented control interfaces
-   AI-assisted compliance checking
-   Engineering decision support

------------------------------------------------------------------------

## Technology / Python Ecosystem

The notebooks use a mixture of standard Python tools and specialist
libraries. Imports found across the notebooks include:

-   **NumPy** --- numerical computation
-   **SciPy** --- optimisation
-   **PyTorch** --- neural-network surrogate modelling
-   **DEAP** --- evolutionary algorithms / NSGA-II
-   **Matplotlib** --- visualisation
-   **Pydantic** --- structured data validation
-   **BAC0** --- BACnet/IP integration in the extended BMS example
-   Python `dataclasses`, `enum`, `json`, `typing`, and related
    standard-library modules

Some notebooks intentionally use **mock/simulated implementations**
rather than live APIs or physical building systems.

------------------------------------------------------------------------

## How to Use the Notebooks

1.  Clone or download this repository.
2.  Open the notebooks with Jupyter Notebook, JupyterLab, or VS Code.
3.  Read the explanatory markdown cells before running the code.
4.  Run the notebooks from top to bottom.
5.  Experiment with the parameters and constraints.
6.  Compare how changing assumptions affects the optimisation or AI
    output.
7.  Treat simulated outputs as demonstrations rather than validated
    engineering results.

For notebooks that reference external systems such as BIM software, LLM
APIs, vector databases, or BACnet devices, the examples may require
additional configuration before they can be connected to real systems.

------------------------------------------------------------------------

## Notes on Scope and Reproducibility

These notebooks represent a **learning portfolio rather than a
production software package**.

In particular:

-   Some LLM/VLM calls are represented by mock functions or simulated
    outputs.
-   Some physical models are simplified or heuristic.
-   BIM quantity extraction is approximated in the generative examples.
-   Compliance rules are illustrative and should not be interpreted as
    legal advice.
-   BACnet interfaces demonstrate the control architecture and should be
    validated in a safe test environment before any real deployment.
-   Real engineering applications would require validated models,
    authoritative data sources, appropriate standards, testing,
    cybersecurity controls, and professional review.

The value of these exercises is therefore primarily in understanding
**how AI techniques can be integrated with conventional engineering
computation and decision-making systems**.

------------------------------------------------------------------------

## Learning Context

These notebooks are part of my broader learning journey through the
**Imperial College London Professional Certificate in Machine Learning /
AI**, supplemented by exercises, examples, and experimentation based on
material encountered online.

They are shared as a record of learning and exploration, with an
emphasis on connecting machine-learning concepts to **architecture,
engineering, BIM, building performance, and building management
systems**.
