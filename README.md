GRAAL
=====

**GRAAL** (Genome Re-Assembly Assessing Likelihood) is a Hi-C data based reassembler written in Python and CUDA. It uses an MCMC (Markov Chain Monte Carlo) method to find and evaluate the most likely genome given a set of genome-wide contact data through a succession of various operations (cut, insert, flip, swap, etc.) performed at various scales based on the initial genome's restriction fragments. A complete description and demonstration are available in full [here](http://www.nature.com/ncomms/2014/141217/ncomms6695/full/ncomms6695.html).

This repo provides the software and the datasets used in the above paper - see [below](https://github.com/koszullab/GRAAL#generating-your-own-datasets) if you want to use GRAAL to reassemble your own genome.

Requirements (Hardware)
-----------------------
- NVIDIA graphic card (computing capability >=2.0, RAM >= 1.5Go)
- Linux (Recommended Ubuntu >= 13.10), OSX, Windows

Requirements (Software)
-----------------------
- hdf5
- hf5py
- CUDA (Cuda Toolkit >= 5.5)
- pycuda (with opengl support)
- OpenGL
- wx
- wxpython
- wxpython-version
- numpy
- matplotlib
- scipy
- PyOpenGL

To install pycuda with opengl support, first, follow the instructions at http://wiki.tiker.net/PyCuda/Installation .
After running "python configure.py" change the file siteconf.py as follows:

Replace:
    CUDA_ENABLE_GL = False 
by:
    CUDA_ENABLE_GL = True

Installation
------------
- Open a terminal
- Create a directory your_dir
- Extract graal.zip to your_dir
- Create a directory your_dir/data 
- Extract fasta.zip, S1.zip and tricho_qm6a to your_dir/data
- cd your_dir/graal
- python main_window.py
- Follow the instructions in the GUI

Description
-----------
([Detailed explanation](https://github.com/koszullab/GRAAL/blob/master/GRAALprinciple.pdf) of GRAAL's algorithm)

A pyramid of contact matrices, P = {M0, M1, ..., Mk}, is a data structure representing the 3C/HiC data at different scales.
The level 0 corresponds to the fragment contact matrix M0. If x is the subsampling/scaling factor, we construct Mi by creating bins of x^i collinear restriction fragments.
G0 is the initial genome used to align the reads.

The following steps refers to numbers and letters indicated in the pdf documents “start_graal.pdf” and “pending_graal.pdf”. 

1) Load data set. 
   
   - Select the folder your_dir/data/S1 or your_dir/data/tricho_qm6a
   
       - size of pyramid = 6 for tricho_qm6a ( t.reesei) 
       - size of pyramid = 4 for S1 ( s.cerevisiae)
       - sub sampling factor = 3

2) Load the corresponding fasta file located in your_dir/data/fasta
3) Build the pyramid
4) Load the pyramid 
5) Click on the "GRAAL" button
6) Fill the parameters
7) Click "start" to begin the simulation, and enter in the terminal the ID of the GPU used for computing.
8) Export trace and histogram of the selected variables



A) The updated contact matrix
B) Real time representation of the genome. Each floating ball corresponds to a bin of restriction fragments
C) Real time visualisation of the parameters of the simulation


The visualisation is made in a 3D OpenGl window.
Left click and drag in the OpenGl window to move into the graph.

Right click and drag to zoom in/out

Press ‘w’ to change the background color

Press 'p' to increase the size of the fragments

Press 'm' to decrease the size of the fragments

Press ‘d’ to decrease the contrast of the matrix

Press ‘b’ to increase the contrast of the matrix

Datasets
--------
- Trichoderma - https://www.dropbox.com/s/ira4j0wrz3sucl8/trichoderma_qm6a.tar.gz
- Cerevisiae - https://www.dropbox.com/s/nx7tzhbzrp1l11t/cerevisiae_malaisyan_strain.tar.gz
- Both genomes - https://www.dropbox.com/s/7nbc3rotu3g8pt4/genomes.tar.gz

Generating your own datasets
----------------------------

If you wish to generate custom datasets in order to reassemble your own genome, you may do so with [HiC-Box](https://github.com/koszullab/HiC-Box) using paired-end read files and FASTA genome as inputs. The so-called pyramid files generated by the box are also used by GRAAL and are treated the same way as the above three datasets.
