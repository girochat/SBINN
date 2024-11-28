# SBINN: Systems Biology-Informed Neural Networks
### Project Overview

This repository contains the code to implement a Systems Biology Informed Neural Network (SBINN), a novel approach inspired from Physics-Informed Neural Networks (PINNs) which integrates scientific knowledge into neural network architectures in the form of ODEs/PDEs. PINNs represent a powerful tool for incorporating mechanistic knowledge from physics with the flexibility and learning capabilities of neural networks. It can be used for forward (dynamics prediction) and reverse modeling (parameter inference), and for equation discovery using additional tools and methods such as SINDy for symbolic regression.  

(PINN schematic)

In this project, several strategies were investigated to improve the convergence of vanilla Physics-Informed Neural Networks (PINNs) with regard to biological systems. In particular, the focus was on adaptive weighting strategies for the multi-component loss function of PINN/SBINNs and addressing convergence issues when increasing the frequency of the target function(s).  
Besides the basic SBINN Implementation which consists in a fully connected feedforward neural network with early stopping and learning rate scheduling, the following algorithms were implemented: 
- ReLoBRaLO: A weight scaling method designed to improve loss component balancing dynamically [[1]](#references).
- Heuristic Loss Normalisation: A custom approach that normalizes each loss component by its mean over the past 1000 iterations, coupled with regularization to prevent trivial constant solutions.
- Importance Sampling: The importance sampling algorithm of Nabian et al. is used to handle convergence challenges with high-frequency input signals [[2]](#references).  

To test the implementation on a biological model, a theoretical model was used to simulate data. It was presented in Chapter 13: Parameter Estimation, Sloppiness, and Model Identifiability by Daniels et al. (2018) in "Quantitative Biology: Theory, Computational Methods, and Models" and consists in a three-tier phosphorylation cascade upon input stimulation with a negative feedback loop [[3]](#references). Here is a schematic of the model:

<p align="center">
<img width="577" alt="Screenshot 2024-11-28 at 14 48 53" src="https://github.com/user-attachments/assets/96fbffed-f4d5-442c-b3b5-bdd3f10b3255">
</p>

### Installation

1. Clone the Repository:

    `git clone https://github.com/girochat/SBINN.git`  
    `cd <path_to_repository>/SBINN`

2. Install Dependencies:  
Use the provided requirements.txt to set up the environment with conda (see [install conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)):  
   conda install -r requirements.txt

### Usage

The code consists into the Jupyter notebook `SBINN.ipynb` that is organised into several sections. To run the notebook, launch Jupyter Lab from the repository
directory:
  `jupyter-lab`

The notebook is structured into three main sections:
- SBINN setup:  
  This section contains all helper functions necessary to plot the results and define the ODE system for the physics component loss. It also contains the model class to define the neural network.  
  &nbsp;
- Data simulation:  
  This section allows to simulate data using the ODE system that will be part of the SBINN architecture. In this notebook, two ODE systems are implemented. The one corresponding to the NFB model introduced above as well as a simple ODE system representing the constant activation of a protein that is triggered by a pulsatile signal.  
  &nbsp;
- Upgrade Algorithms:  
  This section contains the implementation of the algorithms designed to improve the SBINN convergence. There is a dedicated function for the ReLoBRaLo algorithm, the importance sampling algorithm and the heuristic loss normalisation algorithm.  
  &nbsp;
- SBINN training:  
  This final section contains the function implementing the training loop.  
&nbsp;
  

### References

[1]  
[2]
[3]
[4]

### License

This project is licensed under the MIT License. See the LICENSE file for details.
