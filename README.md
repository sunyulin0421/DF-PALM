# DF-PALM
Official implementation: "DF-PALM: Dynamic Fusion Prompt Learning for Audio–Language Models"

***All code, model weights, datasets, and log files have been fully prepared. We commit to releasing them publicly upon paper acceptance and guarantee the reproducibility of the code.***

## :loudspeaker: News:
January 6th, 2026: We submitted our paper DF-PALM to ACL'26 conference

## :information_desk_person: Overview:
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/Flowchart_Asy.png)
***The proposed DF-PALM framework.*** A. Inputs \& Frozen Backbones: Pre-trained audio and text encoders extract initial representations. B. Instance-Aware Context Generation: A learnable Meta\_Net ($g_\phi$) aggregates global audio context via mean pooling to predict instance-specific residuals $\Delta z(x)$. These residuals modulate the learnable static prompts $z_i$ to generate Dynamic Text Guidance. C. Asymmetric Cross-Modal Fusion: To bridge the modality gap, the module treats audio features as Queries and the dynamic text guidance as Keys/Values. Through multi-layer cross-attention, audio representations actively retrieve and align with relevant semantic contexts. Notably, the fusion is asymmetric in that only audio representations are iteratively updated, while text representations remain fixed as conditioning signals. D. Prediction Score: Final predictions are computed via the dot product between the refined audio features and the corresponding dynamic text guidance.

## 🔳 Model:
We have shown the efficacy of DF-PALM and other baselines (ZERO-SHOT, COOP, COCOOP, PALM) using [PENGI](https://github.com/microsoft/Pengi) model.

Download the pre-trained PENGI model using the link provided below and place the checkpoint file at path ***pengi/configs*** (after clonning the repo).
| Model | Link |  Size  |
| --------   | :-----:  | :----:  |
| PENGI | [Download](https://zenodo.org/records/8387083/files/base.pth) |  2.2 GB |

PENGI checkpoint can also be downloaded with following command:
```
wget https://zenodo.org/records/8387083/files/base.pth
```

## 📃 Datasets:
We have performed experiments on 11 audio classification datasets.
| Dataset | Year | Type |  Classes  | Size |
| :-------| :-----:  | :----  | :----: | :----: |
| [Beijing-Opera](https://compmusic.upf.edu/bo-perc-dataset) | 2014  | 	Instrument Classification  | 4 | 69 MB |
| [CREMA-D](https://github.com/CheyneyComputerScience/CREMA-D) | 2014 | Emotion Recognition | 6 | 606 MB |
| [ESC50](https://github.com/karolpiczak/ESC-50) | 2017 | Sound Event Classification | 50 | 881 MB |
| [ESC50-Actions](https://github.com/karolpiczak/ESC-50) | 2017 | Sound Event Classification | 10 | 881 MB |
| [GT-Music-Genre](https://www.kaggle.com/datasets/andradaolteanu/gtzan-dataset-music-genre-classification) | 2012 | Music Analysis | 10 | 1.3 GB |
| [NS-Instruments](https://magenta.tensorflow.org/datasets/nsynth) | 2017 | Instrument Classification | 10 | 18.5 GB |
| [RAVDESS](https://zenodo.org/records/1188976#.YFZuJ0j7SL8)| 2018 | Emotion Recognition | 8 | 1.1 GB |
| [SESA](https://zenodo.org/records/3519845) | 2019 | Surveillance Sound Classification | 4 | 70 MB|
| [TUT2017](https://zenodo.org/records/400515)| 2017 | Acoustic Scene Classification | 15 | 12.3 GB |
| [UrbanSound8K](https://urbansounddataset.weebly.com/urbansound8k.html) | 2014 | Sound Event Classification| 10 | 6.8 GB |
| [VocalSound](https://github.com/YuanGongND/vocalsound) | 2021 | Vocal Sound Classification | 6 | 8.2 GB |

All datasets should be placed in a directory named `Audio-Datasets` and the path of this directory should be specified in the variable `DATASET_ROOT` in the shell `scripts`. Once all datasets have been downloaded, the directory structure should look like as follows:
```
Audio-Datasets/
    ├── Beijing-Opera/
    ├── CREMA-D/
    ├── ESC50/ 
    ├── ESC50-Actions/
    ├── GT-Music-Genre/
    ├── NS-Instruments/
    ├── RAVDESS/
    ├── SESA/
    ├── TUT2017/
    ├── UrbanSound8K/
    ├── VocalSound/
```

## :runner: Run Experiments:
We selected “Apply for the Artifacts Available badge”(Yes) during submission.

We commit to releasing them publicly upon paper acceptance and guarantee the reproducibility of the code.

## :tada: Result:
Comparison of DF-PALM with baselines across 11 datasets. We report the accuracy scores (\%) for all methods. For reproducibility, experiments (except Zero-Shot) were performed using three different random seeds, denoted as S-0, S-1, and S-2. The average score (AVG) is also reported. Bold values indicate the best average performance. Compared to baselines, DF-PALM achieves substantial gains: +8.3\% over CoOp, +5.9\% over CoCoOp, and +2.8\% over PALM.
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/result.png)
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/bar_accuracy_f1_stars.png)

Impact of cross-attention depth ($L$) and width (Heads). The figure comprises four sub-plots: (a-b) Line graphs illustrating the trends in Accuracy and F1-Score; (c-d) Heatmaps highlighting the ``sweet spot'' configuration ($L=3$, 4 Heads) which balances model capacity and overfitting risks.

![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/full.png)

## ❄️ Ablation Studies:
Ablation studies. (\%). w/o Dynamic Context: static prompts + Asymmetric Fusion. w/o Asymmetric Fusion: Dynamic Context + Cosine Similarity.

![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/Ablation_Studies.png)
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/ablation_bar_plot.png)


## :star: Cites:
If you found this repo is helpful, please consider citing our papers:
```
```

## 🙏 Acknowledgement: 
We used [PENGI](https://github.com/microsoft/Pengi) for model instantiation, borrowed some code from [COOP/COCOOP](https://github.com/KaiyangZhou/CoOp) to implement the baseline, and implemented our code based on [PALM](https://github.com/asif-hanif/palm) code. We thank our respective authors for releasing the code.
