# MetaGen

Link to paper: https://arxiv.org/abs/2011.15067


### Overview:


We propose MetaGen, a framework for the unsupervised learning of
metacognition. In MetaGen, metacognition is expressed as a generative model of
how a perceptual system transforms raw sensory data into noisy percepts. Using
basic principles of how the world works (like object permanence), MetaGen jointly 
infers the objects in the world causing the percepts and a representation of its own perceptual system. MetaGen can
then use this metacognition to infer which objects are actually present, thereby
flagging missed or hallucinated objects. On a synthetic dataset of realities and
black-box visual systems, we MetaGen can quickly learn a metacognition
and improve the system’s overall accuracy, outperforming baseline models that lack a metacognition.


The folder METAGEN contains the code for the MetaGen model. The folder ANALYSIS contains the code for analyzing the data. The DATA folder contains the processed data from our 35000 simulations discussed in the paper. It is broken into four chunks to keep the file sizes manageable.

### METAGEN:

To run the MetaGen model on simulated data, run execute_for_NEURIPS.jl. Follow the instructions provided in the comments to name the output csv file and specify the number of percepts to simulate. This execute_for_NEURIPS.jl script will train MetaGen on the simulated percepts. The results will be written to a csv file. If you do this multiple times, with a different name for the output file each time, you can then merge these csv files into one file and then analyze the raw data from MetaGen using the code in the ANALYSIS folder.

### ANALYSIS:

To analyze the processed data that we've provided in the DATA folder file, use the analysis_of_processed_data.R script. This script produces the graphs in Figure 3 of the NEURIPS paper. To analyze raw data output from MetaGen, first merge the .csv files output by each run of run execute_for_NEURIPS.jl. Then analyze the data by running the analysis_of_raw_data.R file. This will process the data and write a new .csv file called ProcessedData.csv. The analysis_of_raw_data.R script will also produce the graphs used in Figure 2 of the NEURIPS paper. This ProcessedData.csv file can then be read in the analysis_of_processed_data.R script.

### Requirements:

METAGEN is implemented in Julia 1.4. It requires the following packages:
* Gen
* FreqTables
* Distributions
* Distances
* TimerOutputs

ANALYSIS is done in R 4.0.0. It requires the following packages:
* tidyverse
* Rfast
* cowplot


### Demos:

Using a real-world artificial visual system, FAIR's Detectron2: https://github.com/facebookresearch/detectron2

#### Demo 1

Output from Detectron2 / Input to MetaGen:

![Alt text](4beii8.gif)

Output from MetaGen (Inferred World States):

![Alt text](4bhqr2.gif)

#### Demo 2

Output from Detectron2 / Input to MetaGen:

![Alt text](4b6dw3.gif)

Detectron2's frame-by-frame outputs were:

[person, bicycle, car]
[person, bicycle, bicycle]
[person, bicycle, bicycle]
[person, bicycle, bicycle]
[person, bicycle, bicycle]
[person, bicycle]
[person, bicycle, motorcycle]
[person, bicycle]
[person, bicycle]
[person, bicycle]

Output from MetaGen (Inferred World States):

![Alt text](4ban7x.gif)

[person, bicycle] for all frames

MetaGen provides a stable representation of the person and the bicycle, and that it infers that the detection of a car and a motorcycle were both hallucinations from the neural net.
