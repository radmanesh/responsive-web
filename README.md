## Project Description: Responsive Webpage Generation and Evaluation using LLMs

This project explores the use of **Large Language Models (LLMs)** for **responsive web design generation**. Inspired by the *Sketch2Code* framework (Li et al., 2024) for sketch-to-HTML translation, this project focuses on generating fully responsive webpages from **three wireframe sketches**—one each for **mobile**, **tablet (iPad Pro)**, and **desktop** layouts.

### Objective

The goal is to develop an **end-to-end pipeline** that:

- Takes **three sketches** (mobile, tablet, desktop) as input, representing layout variations of the same webpage.
- Generates **static HTML with inline CSS**, ensuring responsive behavior without relying on external dependencies.
- **Evaluates** the generated webpages by comparing **rendered screenshots** with **ground truth screenshots** of the original responsive design.

### Pipeline Overview

**Input Representation:**
Each device view is represented by a **full-height wireframe sketch** drawn using standard wireframing conventions (e.g., boxes for images, curly lines for text).

**Code Generation:**
An LLM receives the three sketches and generates an **HTML file with embedded CSS** that scales appropriately across the three target device sizes.

**Evaluation:**
Generated webpages are rendered and compared against reference screenshots using **visual and layout similarity metrics**, such as **Intersection-over-Union (IoU)** and pixel-based similarity.

**LLM as a Judge:**
A secondary evaluation uses **LLMs-as-judges** guided by **three rubrics** (layout accuracy, visual consistency, and cross-device responsiveness) to provide structured qualitative assessments.

### Research Motivation

While *Sketch2Code* (Li et al., 2024) demonstrated the feasibility of converting low-fidelity sketches into webpage prototypes. This project extends that idea by:

- Introducing **multi-device input** for responsive layout synthesis.
- Designing a **quantitative responsive metering system** to evaluate alignment and adaptability across breakpoints.
- Incorporating **LLM-based evaluation rubrics** for standardized assessment across device contexts.

### Expected Outcome

The final system will serve as a **benchmark framework** for **responsive layout generation**, combining **vision-language understanding** and **code synthesis** under realistic design constraints. The evaluation metrics and LLM-based rubrics will contribute to developing more **reliable and standardized measures** for webpage responsiveness in LLM-generated UI code.

- **[ANNOTATOR_GUIDE.md](./ANNOTATOR_GUIDE.md)** - Comprehensive guidelines for creating and annotating responsive wireframes for websites


## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues, fork the repository, and create pull requests.

## 📄 License

Copyright (c) 2025 OUNLP Project Contributors
