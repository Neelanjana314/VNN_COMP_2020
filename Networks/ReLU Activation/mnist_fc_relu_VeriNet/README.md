This folder contains three fully-connected ReLU networks trained with
the MNIST dataset. Also check the dropbox for the latest changes: https://www.dropbox.com/sh/d6q4pbycexizz41/AAAcYN2R6mG2_kQxqZ3Y3i7ra?dl=0

Models are provided in both nnet and ONNX format.  Input images'
pixels are assumed to be floats between 0 and 1. No further
normalisation is required, so lines 4-8 in the nnet files can be
disregarded.

Suggested l_infty constrained permutations for local robustness
benchmarks are:

0.01: Easy (Mostly safe)

0.03: Difficult (Mixed safe and unsafe)

0.05: Intermediate to Difficult (Mostly unsafe) 



50 images and their corresponding labels are drawn from the MNIST test-set in csv format from this folder ; all of the images are classified correctly by all three networks.


I agree that images with long runtimes are more interesting than short runtimes; however, for several use-cases, the verification times for "easy" images are also important. For example, in adversarial training, we may want to use a verification algorithm to locate a large number of unsafe cases but don't really care about precision. The visualisation mentioned above should make it clear whether toolkits perform well for only "easy" or "difficult" cases, so in my opinion, we should include both.


Regarding the reporting, a plot of the number of cases solved as a function of time may be the best way to visualise the results. Plotting safe, unsafe and all epsilons separately is unnecessary; however, it may be better to merge different epsilon values into one plot than merging safe/ unsafe. The reason is that, in my experience, toolkits vary a lot on safe/ unsafe, but usually have a similar relative performance over different epsilon values. 


So one for safe and one for unsafe for each network; resulting in a total of 6 plots for the three networks. One that combines all networks is also a good idea. For the timeout, 60 seconds seems too short.


Steps:
1. Change the epsilon values. I originally suggested 0.01, 0.03 and 0.05. The first is easy and mostly safe, the second is difficult and about 50/50 safe/unsafe and the last is mostly unsafe and easy for some toolkits, difficult for others. Instead, we could use 0.02 (Mostly safe but not as easy as 0.01) and 0.05.
2. Reduce from 50 to 25 input images for each epsilon-network combination.
3. Reduce the timeout to 15 minutes.

This should reduce the worst-case performance to about 1.5 days and I expect all toolkits to finish in less than 1 day.
Having different timeouts for different cases is, in my opinion, unfortunate as it may make the results more difficult to interpret.


  

