# A Large Scale Data-Driven Approach to Estimating Power Generation Costs in AC-OPF Problems
This project leverages large-scale OPFData to predict total power generation cost for AC Optimal Power Flow (AC-OPF) problems using machine learning (ML) techniques. The motivation is to create an efficient, scalable alternative to traditional optimization-based solvers for power systems.

We train models that take only **grid-level features**—representing the physical and operational constraints of a power system—as inputs, and output the **estimated total generation cost**. This approach eliminates the need for solving computationally expensive optimization problems while trying to retain predictive accuracy, especially in large-scale grid settings.
## Background

The Alternating Current Optimal Power Flow (AC-OPF) problem is a fundamental optimization task in power systems, aimed at determining the most cost-effective generation dispatch that meets demand while satisfying operational and physical grid constraints. Solving AC-OPF is computationally intensive, especially in large grids, due to its nonlinear and non-convex nature.

Traditionally, AC-OPF is solved using mathematical programming techniques that do not generalize across instances and require a full re-solve for every change in system conditions. This motivates data-driven approaches that can learn from past solutions to provide faster and scalable cost estimates.

## Problem Statement

Traditional AC-OPF solvers rely on nonlinear optimization techniques, which are often computationally intractable for large and complex power networks.

To address this, our project reframes AC-OPF cost estimation as a **supervised regression problem**. Given a dataset of solved OPF instances, we aim to:
- Learn a mapping from static grid features to total generation cost
- Reduce inference time compared to conventional solvers

## Data Sources and Description 
This project uses the [OPFData dataset](https://doi.org/10.48550/arXiv.2406.07234) [1], a large-scale collection of AC Optimal Power Flow (AC-OPF) problem instances with diverse grid configurations. The dataset is organized into three main components:

- **Grid** – Contains physical and operational parameters of the power system prior to optimization, including bus voltages, generator set points, loads, and transmission line data.
- **Solution** – Stores the post-optimization results, such as power generation levels after solving the OPF problem.
- **Metadata** – Includes the objective value, specifically the total generation cost in \$/h, derived from the OPF solution.

For this project, we focus exclusively on the **grid** and **metadata** components. By excluding the solution data, we ensure that our ML model predicts the total generation cost using only the input grid configuration, avoiding data leakage and improving generalization.

## Repository Structure
```
DS5460_FinalProject/
├── docs/                     # Supporting documentation and figures
├── Milestone1.ipynb          # Initial data exploration and preprocessing
├── Milestone2.ipynb          # More data exploration and cleaning 
├── Milestone3.ipynb          # Feature engineering and hyperparameter tuning
└── finalmilestone.ipynb      # Final model deployment and summary
```
## Installation Instructions

This project is designed to run entirely within a Google Cloud Dataproc environment. Follow the steps below to set up the dataset and run the notebooks.

### 1. Access and Prepare the Dataset

The dataset is hosted in a Google Cloud Storage bucket. To copy it into your own bucket for use in Dataproc:

- Follow the steps in [`docs/EXTRACTION_PROCESS.md`](docs/EXTRACTION_PROCESS.md) to retrieve and organize the dataset.
- Ensure your Google Cloud Storage bucket has appropriate permissions and structure to support access from your Dataproc cluster.

### 2. Launch a Dataproc Cluster

- Use the Google Cloud Console to spin up a **Dataproc cluster** with **Jupyter Notebook** enabled.
- Select appropriate specs (e.g., Python environment, RAM, CPUs) depending on your compute needs.

### 3. Clone the Repository in Jupyter

Once your Dataproc cluster is live:

- Open the **Jupyter Notebook interface**
- Clone this repository directly from within a Jupyter terminal:

```bash
git clone https://github.com/atumlin/DS5460_FinalProject.git
```
### 4. Run the Notebooks
Notebooks are organized by milestone, representing different phases of the project.
- Milestone1.ipynb: Initial data ingestion and analysis 
- Milestone2.ipynb: Data exploration and cleaning
- Milestone3.ipynb: Feature engineering and early modeling
- finalmilestone.ipynb: Final model results and summary

We recommend running the milestone notebooks sequentially for insight into the full process. You may run `finalmilestone.ipynb` to view only the final results.

## Results



## Sample Run and Output 



## Resources 
> S. Lovett et al., “OPFData: Large-scale datasets for AC optimal power flow with topological perturbations,” arXiv preprint arXiv:2406.07234, Jun. 2024. https://doi.org/10.48550/arXiv.2406.07234
