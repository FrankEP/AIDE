# AIDE
AIDE: Annotation-efficient deep learning for automatic medical image segmentation
original paper:https://www.nature.com/articles/s41467-021-26216-9

## Introduction
This is the official code of AIDE, a deep learning framework for automatic medical image segmentation with imperfect datasets, including those having limited annotations, lacking target domain annotations, and containing noisy annotations. Automatic segmentation of medical images plays an essential role in both scientific research and medical care. Deep learning approaches have presented encouraging performances, but existing high-performance methods typically rely on very large training datasets with high-quality manual annotations, which are normally difficult or even impossible to obtain in many clinical applications. We introduce AIDE, a novel annotation-efficient deep learning framework to handle imperfect training datasets.

## Quick start
### Install
1. Install PyTorch=1.1.0 following the [official instructions](https://pytorch.org/).
2. git clone [https://github.com/lich0031/AIDE](https://github.com/lich0031/AIDE).
3. Install dependencies: pip install -r requirements.txt

### Data preparation
- If you want to run the code, you need to download the [CHAOS](https://chaos.grand-challenge.org/), [Prostate dataset domain1 & domain2](https://wiki.cancerimagingarchive.net/display/Public/NCI-ISBI+2013+Challenge+-+Automated+Segmentation+of+Prostate+Structures), [Prostate dataset domain3](https://promise12.grand-challenge.org/Home/), and [QUBIQ](https://qubiq.grand-challenge.org/) datasets for respective tasks.

- Data should be stored in the correct directory tree.

For CHAOS, it should like this:

  $inputs_chaos

  |-- All_Sets  
  |--|--Case_No      
  |--|--|--T1DUAL         
  |--|--|--|--DICOM_anon            
  |--|--|--|--Ground

### Train and evaluate
- Please specify the configuration file.
- For example, train the comparison model on CHAOS with a batch size of 4 on GPU 0:

  python train_files/trainchaos_comparison_1case.py --model_name fuseunet --batch_size 4 --gpu_order 0 --repetition 1

- Model evaluation on the CHAOS dataset can utilize the file train_files/evalchaos_comparison_1cases.py by modifying the image and optimized model path and information accordingly.

### Hardware and time complexities
- To train the model, computers with GPUs should be utilized. The optimization time of the model depends on various factors, including the dataset, the batch size, the epoch number, and the hardware. For our implementation of the CHAOS data, it took the comparison model (984 training samples) around 300s to run one epoch, and it took our framework around 420s. Our framework is a little bit more complex as two models are trained in parallel.
- Installation of the relevant dependencies (e.g. PyTorch) is very fast, taking less than half an hour.
- The models can be evaluated on computers with or without GPU. Evaluation is very fast, and it takes only several seconds to evaluate one 3D image.

## Example results
Example segmentation results on the CHAOS dataset can be found in train_files/examplesegmentationresults. Additional optimized models and segmentation results for the task can be downloaded [here](https://onedrive.live.com/?id=D6A80DBCD21AD447%216335&cid=D6A80DBCD21AD447).
