# DF-PALM
Official implementation: "DF-PALM: Dynamic Fusion Prompt Learning for Audio–Language Models"

***All code, model weights, datasets, and log files have been released. We guarantee the reproducibility of our code and welcome researchers to reproduce our results and conduct follow-up research on our work.***

## :loudspeaker: News:
July 31, 2026: We submitted our paper DF-PALM to AAAI'27 conference(main track)

## :information_desk_person: Overview:
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/Flowchart_Asy.png)
***Overview of the proposed DF-PALM framework.*** (A) Frozen encoders produce the global audio representation and base class representations. (B) The dynamic context generator constructs instance-conditioned class representations. (C) Asymmetric cross-modal fusion refines the audio representation using the conditioned class representations. (D) Similarity scoring produces the classification logits.

## ⚙️ Installation:
1. Create a conda environment
```
conda create --name df_palm python=3.8
conda activate df_palm
```
2. Install PyTorch and other dependencies
```
cd df_palm
pip install -r requirements.txt
```

## 🔳 Model:
We have shown the efficacy of DF-PALM and other baselines (ZERO-SHOT, CoOP, CoCoOP, PALM, FS-AVG, ProKeR) using [PENGI](https://github.com/microsoft/Pengi) model.

Download the pre-trained PENGI model using the link provided below and place the checkpoint file at path ***pengi/configs*** (after clonning the repo).
| Model | Link |  Size  |
| --------   | :-----:  | :----:  |
| PENGI | [Download](https://zenodo.org/records/8387083/files/base.pth) |  2.2 GB |

PENGI checkpoint can also be downloaded with following command:
```
wget https://zenodo.org/records/8387083/files/base.pth
```

## 📃 Datasets:
We have performed experiments on 11 audio classification datasets. Instructions for downloading/processing datasets used by our method have been provided in the DATASETS.md.
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

## ❄️ Code Structure:
There are three main folders in this repo: `pengi`, `df_palm`, `utils`. Code in `pengi` folder is taken from `PENGI` repo for model instantiation. Implementation of baselines (`zero-shot`, `coop`, `cocoop`, `palm`, `fs-avg`, `proker`) and our method `df_palm` is in `df_palm` folder. Class definitions of audio and text encoder of `PENGI` model can be found in `df_palm/encoders.py` file. Training and dataset related code is in `utils` folder.

## :runner: Run Experiments:
We have performed all experiments on `NVIDIA RTX 4090` GPU. Shell scripts to run experiments can be found in `scripts` folder.
```
## General Command Structure
bash  <SHELL_SCRIPT>  <METHOD_NAME>
```

Following methods (including `df_palm`) are supported in this repository:

`zero-shot`, `coop`, `cocoop`, `palm`, `fs-avg`, `proker`, `df_palm`

Examples to run `df_palm` method on different audio classifiction datasets have been provided below:
```
bash scripts/beijing_opera.sh df_palm
bash scripts/crema_d.sh df_palm
bash scripts/esc50_actions.sh df_palm
bash scripts/esc50.sh df_palm
bash scripts/gt_music_genre.sh df_palm
bash scripts/ns_instruments.sh df_palm
bash scripts/ravdess.sh df_palm
bash scripts/sesa.sh df_palm
bash scripts/tut.sh df_palm
bash scripts/urban_sound.sh df_palm
bash scripts/vocal_sound.sh df_palm
```

Results are saved in `json` format in logs directory. To process `results` (take an average across all folds/seeds and print), run the following command (after running all experiments):
```
cd logs
bash results.sh
```

**Note** For multi-fold datasets, we run experiments using cross-validation and then report average results on each seed.

## :tada: Result:
**Complete 16-shot classification accuracy across 11 audio benchmarks.** **a**, Zero-shot and established prompt-learning baselines, comprising **Zero-Shot, CoOp, CoCoOp and PALM**. **b**, Training-free support-set adaptation methods, **FS-AVG (PENGI)** and **ProKeR (PENGI)**, compared with **DF-PALM**. Values are classification accuracies (\%). **S-0--S-2** indicate three matched random seeds that use identical seed-specific, class-wise support subsets across few-shot methods; Zero-Shot is evaluated without support examples. For benchmarks with cross-validation, results are first averaged across folds within each seed. AVG denotes the mean across the three seeds, and AVERAGE denotes the unweighted mean across all 11 benchmarks. Bold values indicate the highest seed-averaged accuracy for each benchmark and the highest overall cross-benchmark mean. FS-AVG and ProKeR construct support-dependent predictors without gradient-based parameter optimization.

![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/result.png)

**Complete 16-shot macro-averaged F1 performance across 11 audio benchmarks.** **a**, Zero-shot and established prompt-learning baselines, comprising **Zero-Shot, CoOp, CoCoOp and PALM.** **b**, Training-free support-set adaptation methods, **FS-AVG (PENGI)** and **ProKeR (PENGI)**, compared with **DF-PALM**. Values are macro-averaged F1 scores (Macro-F1; \%). **S-0--S-2** indicate three matched random seeds using identical seed-specific, class-wise support subsets across all few-shot methods; Zero-Shot is evaluated without support examples. For benchmarks evaluated by cross-validation, scores are first averaged across folds within each seed. AVG denotes the mean across the three seeds, whereas AVERAGE denotes the unweighted mean across all 11 benchmarks. Bold values indicate the highest seed-averaged Macro-F1 for each benchmark and the highest overall cross-benchmark mean. FS-AVG and ProKeR construct support-dependent predictors without gradient-based parameter optimization.

![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/result_f1.png)


## ❄️ Ablation Studies:
Ablation studies validating the components of **DF-PALM** **(%)**. The variant without dynamic context utilizes static prompts coupled with asymmetric fusion. The variant without asymmetric fusion utilizes dynamic context coupled with simple cosine similarity.

![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/Ablation_Studies.png)


## :star: Cites:
If you found this repo is helpful, please consider citing our papers:
```
```

## 🙏 Acknowledgement: 
We used [PENGI](https://github.com/microsoft/Pengi) for model instantiation, borrowed some code from [COOP/COCOOP](https://github.com/KaiyangZhou/CoOp) to implement the baseline, and implemented our code based on [PALM](https://github.com/asif-hanif/palm) code. We thank our respective authors for releasing the code.
