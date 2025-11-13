# Responsive Webpage Generation and Evaluation using LLMs (Sketch2Code-Aligned)

This project extends the *Sketch2Code* framework (Li et al., 2024) to a new benchmark task: **responsive webpage generation from multi-viewport sketches**. While Sketch2Code evaluates single-sketch → single-layout HTML generation, this project investigates whether Large Language Models (LLMs) can synthesize **one responsive webpage** from **three related sketches**—mobile, tablet, and desktop.

---

## 1. Objective

The goal of this project is to build a complete pipeline that:

- Takes **three wireframe sketches**—mobile, tablet, and desktop—representing the same webpage across responsive breakpoints.
- Generates a single **static HTML file with inline CSS** that behaves responsively across all three device sizes.
- Evaluates the generated webpage using:
  - objective **IoU-based layout similarity** for each device (as used in Sketch2Code),
  - perceptual similarity metrics, and
  - **LLM-as-a-Judge** qualitative rubrics designed for responsive behavior.

This creates the first **multi-sketch → responsive-HTML** benchmark aligned with the Sketch2Code methodology.

---

## 2. Pipeline Overview

### 2.1 Input (Aligned with Sketch2Code Data Representation)

Each device view is represented by a **wireframe sketch corresponding to that device’s viewport size**, drawn using standard wireframing conventions:

- boxes with “X” for images
- wavy lines for text
- rectangles for cards, buttons, or sections
- no color or detailed text

This matches the low-fidelity visual abstraction used in Sketch2Code, extended to **three device-specific layouts**.

---

### 2.2 Code Generation (Direct Generation Equivalent)

The three sketches are provided to the LLM in a **single-turn generation setting**, with no multi-turn refinement.
The LLM outputs:

- one **HTML file**, and
- **inline CSS** implementing the responsive behavior (via CSS breakpoints).

The model must infer and encode the layout differences across the three sketches using responsive web design principles.

---

### 2.3 Rendering

The generated webpage is rendered at three device sizes:

- **Mobile:** 375×(page_height)
- **Tablet:** 768×(page_height)
- **Desktop:** 1280x(page_height)

Screenshots from each viewport are saved for evaluation, consistent with Sketch2Code’s screenshot-based metric pipeline.

---

## 3. Evaluation Framework (Extended from Sketch2Code)

### 3.1 Objective Metrics

#### A. IoU-Based Layout Similarity
Using Sketch2Code’s methodology, we extract visual components for each viewport:

- text blocks
- images
- navigation bars
- buttons
- forms/tables
- dividers
- tertiary components

For each component type, we compute:

IoU = area_overlap / area_union

This produces **three layout similarity scores**, one per device.

#### B. Perceptual Similarity
Supporting metrics inspired by Sketch2Code:

- block similarity
- text region similarity
- positional alignment
- CLIP similarity

These help detect structural and perceptual correspondence.

---

### 3.2 LLM-as-a-Judge (Human-Aligned Evaluation)

We adopt Sketch2Code’s human-aligned evaluation style but extend it for responsiveness.
Three rubrics are used:

#### Rubric 1 — Layout Accuracy (Per Device)
Checks component presence, ordering, and structural fidelity relative to each sketch.

#### Rubric 2 — Visual Hierarchy & Spacing
Evaluates grouping, spacing, alignment, and proportional scale.

#### Rubric 3 — Cross-Device Responsive Consistency
Ensures that responsive behavior is correct across breakpoints, including:

- stacking/reflow accuracy
- alignment of layout transitions with the sketches
- absence of visual breakage

---

## 4. Responsive Metering System (Composite Metric)

To unify the evaluation, we introduce the **Responsive Meter**:

ResponsiveMeter =
w1 * Avg(IoU_mobile, IoU_tablet, IoU_desktop)
	•	w2 * CrossDeviceConsistency
	•	w3 * LLMJudgeScore
	•	w4 * PerceptualSimilarity

This metric captures:

- per-device fidelity
- cross-breakpoint behavioral correctness
- qualitative assessment
- visual-likeness

---

## 5. Research Motivation

Sketch2Code identifies major challenges for current VLMs: spatial reasoning, layout fidelity, and structural hallucination.
However, Sketch2Code evaluates only **static webpage generation from a single sketch**.

This project extends that framework to:

1. **Multi-sketch conditioning for responsive design**
   Reflects real-world workflows where different device breakpoints have different layouts.

2. **One-shot responsive generation**
   Requires synthesizing three layouts into one code artifact.

3. **Cross-device evaluation metrics**
   Extends Sketch2Code’s IoU metric to multiple viewport evaluations.

4. **Responsiveness-aware qualitative evaluation**
   Captures the correctness of layout transitions between viewports.

---

## 6. Expected Outcome

This project will produce:

- A **dataset of mobile/tablet/desktop sketch triplets**
- A **standardized generation prompt**, compatible with Sketch2Code
- A **responsive evaluation suite** extending IoU and perceptual metrics
- A **rubric-based judging system** for responsive fidelity
- A unified **Responsive Meter** for overall scoring

Together, these create the first systematic benchmark for **LLM-generated responsive webpages**, rooted in the rigor of the Sketch2Code evaluation framework.