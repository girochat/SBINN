# SBINN: Systems Biology-Informed Neural Networks
### Project Overview

This repository contains the code to implement a Systems Biology Informed Neural Network (SBINN), a novel approach inspired from Physics-Informed Neural Networks (PINNs) which integrates scientific knowledge into neural network architectures in the form of ODEs/PDEs. PINNs represent a powerful tool for incorporating mechanistic knowledge from physics with the flexibility and learning capabilities of neural networks. It can be used for forward (dynamics prediction) and reverse modeling (parameter inference), and for equation discovery using additional tools and methods such as SINDy for symbolic regression.  

<p align="center">
<img width="578" alt="sbinn_schematic" src="https://github.com/user-attachments/assets/08b7ded0-cd80-4118-88a8-deb7ab11b1b2">
</p>

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
  This section contains the function implementing the training loop.  
&nbsp;
- Plotting and Saving:
  This final section allows to visualise the results such as the final functions approxiated by the neural network and the progress of each loss component. It offers also the possibility to save the model along with some characteristic elements.
&nbsp;

### Repository Content

- **Data**:  
  This folder contains the data that was simulated using the NFB model and that was used to test the implementations and train the SBINN.
- **Plots**:  
  This folder contains the plot of the final prediction of a given configuration of the SBINN as well as the plot of the loss progress for each loss component.
- **Model**:
  This folder contains the data of all models that were trained. After loading, it can contain information about the model parameters, the final epoch, the early stopping patience or learning rate scheduler characteristics depending on the case.


### References

[1]  Bischof and Kraus (2021). Multi-Objective Loss Balancing for Physics-Informed Deep Learning. [DOI](https://doi.org/10.48550/arXiv.2110.09813)  
[2]  Nabian et al. (2021). Efficient training of physics-informed neural networks via importance sampling. [DOI](https://doi.org/10.48550/arXiv.2104.12325)  
[3]  Daniels et al. (2018). Chapter 13: Parameter Estimation, Sloppiness, and Model Identifiability in "Quantitative Biology: Theory, Computational Methods, and Models".   

### License

This project is licensed under the MIT License. See the [license file](LICENSE.txt). file for details.
