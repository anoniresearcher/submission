# Reproducibility

This repository contains information and material to reproduce the experiments of our ICDE 2021 submission. 

Refer to ```all_classifiers_and_synthetic_generators.txt``` for all the classifiers and synthetic generators configurations, which allows for reproducing all experiments in the paper. The ```\datasets``` directory contains all real and reshuffled datasets. 

Requirements: 
* You will need JAVA 8 or 9 installed. 
* moa-SLEADE.jar is required and it can be found in the directory with this README. 
* The datasets are also available at the root of this directory. 
* Information about how to execute MOA can be found in [here](https://moa.cms.waikato.ac.nz/getting-started/)

The example below executes SLEADE on the AGRa dataset. To produce the same result as shown in the **warm-up and online** scenario using 10 learners. Repeat the same command varying the random seed (parameter **-r**) from 1 until 5. The accuracy presented in Table 2 is the average *classifications correct (percent)*

PS: The AGRa is a synthetic dataset, thus this command also generate the data. 

This command can be run from the command line: 
```
  java -cp moa-SLEADE.jar moa.DoTask "EvaluateInterleavedTestThenTrainSSLDelayed -b trees.HoeffdingTree -l (semisupervised.Lead -l (StreamingRandomPatches -s 10 -u -q) -b ArgMax -q -p MultiViewMinKappaConfidence -m 0.0 -t MajorityTrainsMinority -s -v) -s (ConceptDriftStream -s generators.AgrawalGenerator -d (ConceptDriftStream -s (generators.AgrawalGenerator -f 2) -d (ConceptDriftStream -s generators.AgrawalGenerator -d (generators.AgrawalGenerator -f 4) -p 25000 -w 50) -p 25000 -w 50) -p 25000 -w 50) -j 0.99 -k 1 -w -i 100000"
```

Optionally, the command can be copied and pasted in the MOA GUI. Use the following command in the command line to invoke the GUI. 
To run the MOA GUI, execute the following command in the command line:

```
java -cp moa-SLEADE.jar moa.gui.GUI
```

This is the command to be copied into the MOA gui (no line breaks): 
```
EvaluateInterleavedTestThenTrainSSLDelayed -r 1 -l (semisupervised.Lead -l (StreamingRandomPatches -s 10 -u -q) -b ArgMax -q -p MultiViewMinKappaConfidence -m 0.0 -t MajorityTrainsMinority -s -v) -s (ConceptDriftStream -s generators.AgrawalGenerator -d (ConceptDriftStream -s (generators.AgrawalGenerator -f 2) -d (ConceptDriftStream -s generators.AgrawalGenerator -d (generators.AgrawalGenerator -f 4) -p 25000 -w 50) -p 25000 -w 50) -p 25000 -w 50) -j 0.99 -k 1 -w -i 100000
```
