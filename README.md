# ParticleSwarmOptimization

implementation of the particle swarm algorithm to optimize the paramters and Input Variables of TMVA Classificators.  
The program will create a swarm of Classifiers in the paramter space.  
Each classifier will try to improve its input variable combination.  
Classifiers move in the paramter space using the information of the whole swarm.  
Utilizes batch system to parallelize classifier training.  


1) clone the repository  

2) The python interface manages the communication between the particles and is run on a portal (use screen because of long    runtimes).  
The Training of the BDTs is done on the batch system and is implemented in Particle.C. This file is also recompiled when you start the PSO now.

3) change Example_PSOConfig to suit your needs  
     should work on ekp and NAF batch system, for other batch system change PSO/QueHelper.py  
     play around with the swarm parameters (15 to 25 particles recommended)  
     choose the Figure of Merit to optimize (at the moment ROC or experimentally the chi of a b-only fit)  
     specify TMVA factory and method options  
     declare coordinate space you want to search  
     specify Signal and Background trees   
     Variables the swarm starts with   
     pool of additional Variables the swarm will try  

4) Setup environment with 
    ```
    source setup.sh
    ```
5) Start the Optimization with  
    ```
    python runPSO.py -c config_bb4l_ATLAS/PSOConfig_bb4l.txt -o bb4l_Output
    ```
    The PSO will start one job that submits and monitors HTCondor jobs to find the optimized settings.
    The `watcher job` should be run in `screen` or `nohup`:
    ```
    nohup python runPSO.py -c config_bb4l_ATLAS/PSOConfig_bb4l.txt -o bb4l_Output_2016 --verbose >& optimize_BDT.out &
    ```
    
6) After each iteration the ten best classifiers are writen to PSOResult.txt  
   The best classifier and all necessary information is written to a file starting with "FinalMVAConfig_"  
   
   
