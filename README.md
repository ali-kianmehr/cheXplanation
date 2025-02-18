![LOGO](/img/CheXplanation.svg)

This the code repo referenced in the paper, "Benchmarking saliency methods for chest X-ray interpretation ". We provided the source code used for evaluation of saliency map localization. To download the validation dataset or view and submit to the leaderboard, visit the [CheXplanation website](https://stanfordmlgroup.github.io/competitions/chexplanation/).

Typical install time: ~5 minutes
Expected run time for demo: ~20 minutes

### Table of Contents

- [Prerequisites](#prereqs)
- [Generate Segmentations from Saliency Heatmap](#segm)
- [Evaluation of Localization](#eval)
- [License](#license)
- [Citing](#citing)

---

<a name="prereqs"></a>

## Prerequisites

The code should be run using Python 3.7.6.

Before starting, please install the repo Python requirements using the following command:
```
pip install -r requirements.txt
```

<a name="segm"></a>

## Generate Segmentations from Saliency Heatmap
We provided the code to generate binary segmentations from saliency heatmaps using a thresholding scheme. The technical details can be found in the Method section of our paper manuscript. To save the binary segmentations efficiently, we used RLE format for storage and the encoding is implemented using the toolbox provided in COCO detection challenge, [pycocotools](https://github.com/cocodataset/cocoapi/tree/master/PythonAPI/pycocotools).


```
python segmentation/pred_segmentation.py [OPTIONS]

Options:
--phase			Use validation or test data
--method   		The saliency methods used
--model     		Single or ensemble
--if_threshold 		Whether the thresholding scheme is adopted.
--save_dir 		Path where the RLE-formatted segmentations are stored.
```

<a name="synthetic"></a>

## Evaluating Localization using Semantic Segmentation Scheme.

Our evaluation script generates the two summary metrics (mIoU and hit rate) for each localization task, as well as the corresponding 95% bootstrap confidence interval (n_boostrap_sample = 1000). 

### Usage

```
Usage: python eval_miou.py [OPTIONS]

Options:
    --phase      	Use validation or test data.
    --save_dir 		Path to which the summary csv is stored.
```

```
Usage: python eval_ptgame.py [OPTIONS]

Options:
    --phase      	Use validation or test data.
    --save_dir 		Path to which the summary csv is stored.
```


<a name="license"></a>

## License

This repository is made publicly available under the MIT License.

<a name="citing"></a>

## Citing

If you are using the CheXphoto dataset, please cite this paper:

```
@article {Saporta2021.02.28.21252634,
	author = {Saporta, Adriel and Gui, Xiaotong and Agrawal, Ashwin and Pareek, Anuj and Truong, Steven QH and Nguyen, Chanh DT and Ngo, Van-Doan and Seekins, Jayne and Blankenberg, Francis G. and Ng, Andrew Y. and Lungren, Matthew P. and Rajpurkar, Pranav},
	title = {Benchmarking saliency methods for chest X-ray interpretation},
	elocation-id = {2021.02.28.21252634},
	year = {2021},
	doi = {10.1101/2021.02.28.21252634},
	publisher = {Cold Spring Harbor Laboratory Press},
	abstract = {Saliency methods, which {\textquotedblleft}explain{\textquotedblright} deep neural networks by producing heat maps that highlight the areas of the medical image that influence model prediction, are often presented to clinicians as an aid in diagnostic decision-making. Although many saliency methods have been proposed for medical imaging interpretation, rigorous investigation of the accuracy and reliability of these strategies is necessary before they are integrated into the clinical setting. In this work, we quantitatively evaluate three saliency methods (Grad-CAM, Grad-CAM++, and Integrated Gradients) across multiple neural network architectures using two evaluation metrics. We establish the first human benchmark for chest X-ray interpretation in a multilabel classification set up, and examine under what clinical conditions saliency maps might be more prone to failure in localizing important pathologies compared to a human expert benchmark. We find that (i) while Grad-CAM generally localized pathologies better than the two other saliency methods, all three performed significantly worse compared with the human benchmark; (ii) the gap in localization performance between Grad-CAM and the human benchmark was largest for pathologies that had multiple instances, were smaller in size, and had shapes that were more complex; (iii) model confidence was positively correlated with Grad-CAM localization performance. Our work demonstrates that several important limitations of saliency methods must be addressed before we can rely on them for deep learning explainability in medical imaging.Competing Interest StatementThe authors have declared no competing interest.Funding StatementN/AAuthor DeclarationsI confirm all relevant ethical guidelines have been followed, and any necessary IRB and/or ethics committee approvals have been obtained.YesThe details of the IRB/oversight body that provided approval or exemption for the research described are given below:The project did not involve human subjects researchI confirm that all necessary patient/participant consent has been obtained and the appropriate institutional forms have been archived, and that any patient/participant/sample identifiers included were not known to anyone (e.g., hospital staff, patients or participants themselves) outside the research group so cannot be used to identify individuals.YesI understand that all clinical trials and any other prospective interventional studies must be registered with an ICMJE-approved registry, such as ClinicalTrials.gov. I confirm that any such study reported in the manuscript has been registered and the trial registration ID is provided (note: if posting a prospective study registered retrospectively, please provide a statement in the trial ID field explaining why the study was not registered in advance).YesI have followed all appropriate research reporting guidelines and uploaded the relevant EQUATOR Network research reporting checklist(s) and other pertinent material as supplementary files, if applicable.YesCheXpert data is available at https://stanfordmlgroup.github.io/competitions/chexpert/. The validation set and corresponding benchmark radiologist annotations will be available online for the purpose of extending the study. https://stanfordmlgroup.github.io/competitions/chexpert/},
	URL = {https://www.medrxiv.org/content/early/2021/10/08/2021.02.28.21252634},
	eprint = {https://www.medrxiv.org/content/early/2021/10/08/2021.02.28.21252634.full.pdf},
	journal = {medRxiv}
}

```

 
