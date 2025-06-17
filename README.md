# De-novo-molecules-design-based-on-molecular-properties
This project implements a Conditional Variational Autoencoder (CVAE) for generating novel molecules (represented as SELFIES sequences) conditioned on desired molecular properties. The model is designed for de novo molecular design and learns to reconstruct and generate molecular sequences guided by physicochemical properties
🧠 Model Overview
The core of the model is a sequence-to-sequence CVAE architecture that:

Encodes SELFIES token sequences into a latent space,

Conditions on molecular properties (e.g., molecular weight, LogP, QED, etc.),

Decodes latent vectors into new molecular sequences.

Components
Property Encoder: Dense neural network that projects molecular property vectors to a latent conditioning vector.

Sequence Encoder: Bidirectional LSTM-based encoder for tokenized SELFIES.

Latent Sampling: Reparameterization trick (z = μ + σ * ε) to allow gradient flow through stochastic nodes.

Decoder: LSTM-based conditional decoder that reconstructs the original SELFIES sequence.

🔄 Workflow
Input
SELFIES sequences: Tokenized molecular structures.

Molecular properties: Normalized continuous descriptors (e.g., MW, LogP).

Output
Reconstructed SELFIES sequence (during training).

Generated novel SELFIES sequences (during inference/generation phase).

📁 Directory Structure
kotlin
Copy
Edit
project/
├── denov_design_molecular_properties.ipynb
├── README.md
├── data/
│   ├── selfies_sequences.txt
│   └── molecular_properties.csv
└── models/
    └── saved_model.h5
🧪 Example Use Case
The model is trained to generate molecules with specific target properties like:

High drug-likeness (QED)

Low or high logP

Specific molecular weights

You can supply a vector like [MW=350, LogP=3.2, QED=0.89, TPSA=75] and the model generates molecules that approximately match these properties.

🧰 Requirements
Install the dependencies via pip:

bash
Copy
Edit
pip install -r requirements.txt
Or manually install:

bash
Copy
Edit
pip install selfies pandas numpy matplotlib seaborn scikit-learn tensorflow
Minimum Requirements
Python >= 3.7

TensorFlow >= 2.10

selfies library for SELFIES tokenization

RDKit (optional, for visualization and property calculation)

🔍 Notebook Summary
The denov_design_molecular_properties.ipynb includes:

Data Loading: Parses molecular properties and SELFIES sequences.

Preprocessing: Tokenizes sequences, normalizes properties.

Model Definition:

Property encoder

CVAE model

Training Loop:

Uses teacher forcing and KL annealing

Tracks reconstruction loss and KL divergence

Evaluation:

Visualizes training history (MAE, MSE)

Samples and decodes new molecules

Visualization:

Compares generated vs. input molecules

Plots latent space dynamics

🧪 Model Performance Metrics
Reconstruction Accuracy: ~85–90% valid molecules depending on training epochs.

Property MAE: < 0.1 for most standardized properties.

KL Divergence: Monitored with β scheduling for smooth latent space learning.

🚀 How to Generate Molecules
python
Copy
Edit
# Given a property vector:
target_properties = ([[Molecular weight, HBD, HBA, Number of rotatable bonds, TPSA, Number of atoms]])  # Normalized
generated_selfies = cvae_model.sample(target_properties)
You can visualize the generated molecule using RDKit + py3Dmol if required.

📚 References
Lim et al., "Molecular generative model based on conditional variational autoencoder for de novo molecular design." Journal of Cheminformatics (2018).

SELFIES: https://github.com/aspuru-guzik-group/selfies

