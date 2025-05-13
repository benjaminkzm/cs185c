# Modeling Surface Stratification and Deep Convection in the Labrador Sea

This project explores how **surface ocean conditions affect deep water formation** in the **Labrador Sea**, an important area for the Earth's climate system. Water sinking in this region helps power the **Atlantic Ocean’s circulation**, which moves heat and salt around the globe. The model runs for one full year using **MITgcm**, a realistic ocean simulation that includes ocean depth, weather patterns, and average boundary conditions.

## Science Question

**What does surface temperature variability tell us about the potential for deep water formation in the Labrador Sea?**

## Key Analyses

To answer the science question, this project analyzes output from the model by focusing on four key processes:

### Sea Surface Temperature (SST)
Seasonal SST maps reveal that the surface **cools significantly during winter**, creating dense surface water favorable for vertical mixing. In summer, surface warming leads to **strong stratification** that prevents mixing.

### Mixed Layer Depth (MLD)
A time series of MLD at a central location shows **deep mixing (>2500 m)** in winter, followed by **very shallow layers in summer** due to surface warming and stabilization.

### Vertical Temperature Profiles
Vertical sections of temperature show **how stratification develops with depth and latitude**, highlighting the central Labrador Sea as the main region of active convection.

### Vertical Velocity
2D maps and time–depth plots of vertical velocity confirm the **timing and depth of sinking motion**, providing direct evidence of **deep convection events** in late winter and early spring.

## Reproducing Model Results

*Note for CS185C: The following section outlines possible steps that may be included in your README for reproducibility. When designing your own steps, be sure to consider which of the steps below pertain to your model and update/modify accordingly.*

### Step 1: Create Input Files

Generate the following input files using the provided notebooks:

- **Model Grid**  
  `notebooks/Creating the Model Grid.ipynb`
- **Bathymetry**  
  `notebooks/Creating the Bathymetry.ipynb`
- **Initial Conditions**  
  `notebooks/Creating the Initial Conditions.ipynb`
- **External Forcing Conditions**  
  `notebooks/Creating the External Forcing Conditions.ipynb`
- **Boundary Conditions**  
  `notebooks/Creating the Boundary Conditions.ipynb`

Place all generated files in the `input/` directory.

### Step 2: Transfer Files to the Computing Cluster

Clone MITgcm and prepare a config folder:

```bash
git clone https://github.com/MITgcm/MITgcm.git
mkdir MITgcm/configurations/labrador_sea
```
Then, use the **scp** command to send the **code**, **input**, and **namelist** directories to your configuration directory.

### Step 3: Compile the Model

Once all of the files are on the computing cluster, the model can be compiled. Make a build directory in the configuration directory and run the following lines:

```bash
mkdir build
cd build
export MPI_HOME=/home/cs185c08/.conda/envs/cs185c
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make
```

### Step 4: Run the Model
After the compilation is complete, move to the run directory, link everything from input and code, and the submit the job script:

```bash
sbatch cs185c.slm
```

### Step 5: Analyze the Results

Use the provided Jupyter notebooks:

1. notebooks/Analyzing Model Results.ipynb

   View SST evolution, generate animations, and assess seasonal signals.

2. notebooks/Answering the Science Question.ipynb

   Recreate MLD time series, temperature sections, vertical velocity plots, and interpret convection patterns.