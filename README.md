# DF-PALM
Official implementation: "DF-PALM: Dynamic Fusion Prompt Learning for Audio–Language Models"

***We selected “Apply for the Artifacts Available badge”(Yes) during submission.***

***All code, model weights, datasets, and log files have been fully prepared. We commit to releasing them publicly upon paper acceptance and guarantee the reproducibility of the code.***

## :loudspeaker: News:
October 8th, 2025: We submitted our paper DF-PALM to WWW'26 conference

## :information_desk_person: Overview:
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/flowchart.png)
***Illustrates the proposed DF-PALM framework.***

## :runner: Run:
We selected “Apply for the Artifacts Available badge”(Yes) during submission.

We commit to releasing them publicly upon paper acceptance and guarantee the reproducibility of the code.

## :tada: Statistic:
Comparison of DF-PALM with Baselines. The accuracy scores of the methods (ZERO SHOT, COOP, COCOOP, PALM and our proposed method DF-PALM) across 11 datasets are presented. For each method (except ZERO SHOT), experiments were performed using three different seeds. The accuracy scores for all seeds are reported, along with the average score. Bold values indicate the best average score in each row. Compared to the baselines, our proposed method achieves favorable results, with an average improvement of 8.3% over COOP, 5.9% over COCOOP and 2.8% over PALM.
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/result.png)
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/bar_accuracy_f1_stars.png)

The impact of different numbers of layers and heads in the cross-attention module on model performance.

![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/full.png)

## ❄️ Ablation Studies:
Ablation studies. Among them, w/o Dynamic Context represents DF-PALM removing the context generator and only using cross-attention; w/o Cross-Attention represents the retention of the dynamic context generator without going through the cross-attention module.
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/Ablation_Studies.png)
![image](https://github.com/sunyulin0421/DF-PALM/blob/main/Illustration/ablation_bar_plot.png)


## Cites: :star:
If you found this repo is helpful, please consider citing our papers:
```
```
