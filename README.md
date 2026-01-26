# VCREASONER: Mechanistic Reasoning Traces Dataset

A dataset of structured mechanistic reasoning traces for virtual cell reasoning. VCREASONER provides a multi-agent framework to understand and predict how biological perturbations (drugs, gene knockouts, etc.) affect cells at a mechanistic level.

## Dataset Overview

The dataset contains **18,950 mechanistic reasoning traces** that explain:
- How drugs/compounds affect specific cell types
- The molecular mechanisms involved (binding, enzymatic reactions, signaling cascades)
- Predicted phenotypic outcomes

Each trace includes:
- **Human-readable reports** - Detailed mechanistic explanations in markdown
- **Structured explanations** - Formalized action primitives describing molecular events
- **Causal graphs (DAGs)** - Directed acyclic graphs showing cause-effect relationships

## Installation

```bash
# Clone the repository
git clone https://github.com/yunhuijang/VCReasoner.git
cd vcreasoner

# Create virtual environment with uv
uv sync
```

## Quick Start

See the demo notebook at `notebook/demo.ipynb` for a complete walkthrough.

```python
import pandas as pd

# Load the dataset
df = pd.read_parquet('data/vc_traces.parquet')

print(f"Dataset shape: {df.shape[0]:,} traces, {df.shape[1]} columns")
# Output: Dataset shape: 18,950 traces, 6 columns
```

## Dataset Schema

| Column | Description |
|--------|-------------|
| `perturbation` | Dict containing the cellular context (cell type, etc.) and perturbation details (compound, targets, etc.) |
| `question` | The mechanistic question posed about the perturbation's effects |
| `report_text` | Human-readable mechanistic report in markdown format |
| `explain` | Structured explanation using action primitives |
| `dag` | Directed acyclic graph edges defining causal/correlative relationships |
| `explain_verified` | Verified/filtered version of the structured explanation |

## Action Primitives

The structured explanations use a vocabulary of action primitives to describe mechanistic events:

| Primitive | Description |
|-----------|-------------|
| `set_context()` | Establishes the biological context (cell type, genotype, disease state) |
| `binds_to()` | Drug-target or protein-protein binding with specified affinity |
| `modulates_molecule_activity()` | Changes in protein/enzyme activity (inhibition/activation) |
| `modulates_complex()` | Formation or dissociation of protein complexes |
| `converts_substrate()` | Enzymatic reactions converting substrates to products |
| `regulates_expression()` | Gene expression changes via transcription factors |
| `localises_to()` | Protein/molecule translocation between cellular compartments |
| `post_translational_modification()` | Protein modifications (phosphorylation, cleavage, etc.) |
| `modulates_pathway_activity()` | Pathway-level effects on signaling cascades |
| `induces_phenotype()` | Phenotypic outcomes (growth inhibition, apoptosis, etc.) |

## Project Structure

```
vcreasoner/
├── data/
│   └── vc_traces.parquet    # Main dataset
├── notebook/
│   └── demo.ipynb           # Interactive demo notebook
└── README.md
```
