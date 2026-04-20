PRITHVI DHANABAL ECE570 FINAL PROJECT: MIXUP TINYREPRODUCTION  

README FILE  

Code Structure:  

The code is a .ipnyb notebook, and text headers denoting each section are present in the file itself. 
Imports: This section contains all imports required for the project code to run  

Experiment-Specific Functions: This section defines the training data label corruption function and the mixup data augmentation functions.  

Get Datasets: This section defines batch size, downloads and transforms the PyTorch FashiomMNIST datasets, and finally loads them into DataLoader objects  

Define NN: This section defines the Convolutional Neural Network (CNN), including the layers and forward pass instructions  

Train & Test Functions Mixup: This section contains the training and testing loops for testing with the Mixup methodology, thus calling the Mixup augmentation functions every batch.  

Train & Test Functions ERM: This section contains the standard training and testing loops for testing
Comparison Test & Training Functions: This section contains a wrapper function that automates running the Mixup and ERM test/train loops and collecting performance and computational cost data (GPU usage and runtime)  

Plotting Function: This section contains a function that takes in epoch-series error, runtime and GPU usage data to plot them with the ERM and Mixup curves/bars appearing superimposed on one subplot per metric. Various single-figure metrics: runtime, final error, best error, and average GPU usage, are shown for both ERM and Mixup.   

Run Functions: This section contains the calls to the runscript wrapper function in 7, plotting function in 8, and generation of corrupted-label data performed for this experiment. It is recommended to run one pair (call to wrapper function + call to plotting function) at a time  

Dependencies  

Python 3.latest
PyTorch (handled in imports)
NumPy (handled in imports)
MatPlotLib (handled in imports)
Time, PsUtil, OS, Copy (handled in imports)
TorchAttacks (download and import handled in imports)
Google Colab or other way of running .ipnyb files  

Instructions to Run:  

The following instructions assume that FashionMNIST will remain the dataset of choice. If not, the dataset download as described in Section 3 must be altered.  

The easiest way to run the project is to call the “runscript” wrapper function. This function takes in required inputs of an alpha value for the Mixup augmentation, DataLoaders for the training and testing data, and an epoch count. The output will need to be assigned to an array of eight variables: one for ERM training accuracy, testing accuracy, GPU usage, then the same for Mixup, followed by ERM and Mixup runtimes. This vector can be sent as-is as an input to the plotting function. An example pair of calls is posted below:  

[train_accs, test_accs, max_gpu, train_accs_mixup, test_accs_mixup,
 max_gpu_mixup, elapsed, elapsed_mixup] = runscript(0.25, train_batch, test_batch, batches)  
 
plotting(train_accs, test_accs, max_gpu, train_accs_mixup, test_accs_mixup, max_gpu_mixup, elapsed, elapsed_mixup, batches)  

To test on adversarial examples, after all required inputs to the runscript, add “adv=True” as another input. This flag should also be added to the plotting function’s inputs. To train on corrupted data labels, you must generate DataLoaders with corrupted data, then pass those to the standard runscript, and pass the corruption rate to the plotting function as well. An example generation of corrupted-data DataLoaders is below:  

#Corrupt labels at 20% rate  

[train_20, real_20] = corrupt_labels(copy.deepcopy(train_in), 0.2)
train_batch_20 = torch.utils.data.DataLoader(train_20, batch_size=b_size, shuffle=True)  


NOTE: Please ONLY RUN ONE COMPARISON AT A TIME! THE PLOTTING FUNCTION IS ONLY DESIGNED FOR ONE COMPARISON AT A TIME. Calls to produce all figures in report are present in Section 9, comment/uncomment as needed  

Code Credit Breakdown  

Below is a section-wise detailing of code sources, including links to any external adapted code.  

Imports: All code was written by me  

Experiment-Specific Functions  

corrupt_labels: All code was written by me  

mixup_data: This code was adapted from the original implementation found at the following source: https://github.com/facebookresearch/mixup-cifar10/blob/main/train.py, lines 119-134  

mixup_f: This code was adapted from the original implementation found at the following source: https://github.com/facebookresearch/mixup-cifar10/blob/main/train.py, lines 137-138.  

Get Datasets: All code was written by me  

Train & Test Functions Mixup: This code was adapted from my solution to ECE570 HW2, Exercise 2 Task 1 lines 1-84  

The FGSM attack from TorchAttacks on line 45 of this section was implemented referencing documentation at https://adversarial-attacks-pytorch.readthedocs.io/en/latest/attacks.html#module-torchattacks.attacks.fgsm  

Train & Test Functions ERM: This code was adapted from my solution to ECE570 HW2, Exercise 2 Task 1 lines 1-84  

The FGSM attack from TorchAttacks on line 39 of this section was implemented referencing documentation at https://adversarial-attacks-pytorch.readthedocs.io/en/latest/attacks.html#module-torchattacks.attacks.fgsm  

Runscript: All code was written by me except:  

The initialization of an FGSM attack on lines 13 and 36 were implemented referencing documentation at https://adversarial-attacks-pytorch.readthedocs.io/en/latest/attacks.html#module-torchattacks.attacks.fgsm  

Plotting Function: All code was written by me  

Run Functions: All code was written by me  

