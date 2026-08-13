<div align=center>

<img width="1280" height="640" alt="21433757-bbcc-4ba5-9b0c-ca9c309b79ef" src="https://github.com/user-attachments/assets/1a96dc83-3277-4b91-a7d7-8ed0a6aa4e4c" />

<br>

A research project submitted as a part of the completion of [Kujenga AI Course](https://kujenga.readthedocs.io/en/latest/index.html).

Authored by Henry Ssenono 

</div>

> [!IMPORTANT]
> 
> *Special thanks to the [course instructors for designing a curriculum](https://github.com/AfricaEuropeCoreAI/Kujenga) that made ideas like PageRank, epidemic modelling, and regression feel not just learnable but genuinely applicable to questions that matter close to home.*


## Overview

Social connections across national borders can provide insight into how countries are socially integrated within regional and global networks. 
This project uses the Facebook Social Connectedness Index (SCI) to examine the position of Uganda within these networks, using Kenya as a comparison because both countries are located in East Africa but may occupy different positions within the wider African social network.

The study looks at social connectedness from two perspectives. 
- First, it examines the relative importance of Uganda and Kenya within the African network.
- Second, it investigates whether Uganda and Kenya differ significantly in their social connectedness to countries around the world.

## Research Hypothesis

The network analysis is used to compare the relative importance of Uganda and Kenya within Africa. 
For the global comparison, the study tests whether the two countries differ significantly in their social connectedness.

- Null hypothesis (H<sub>0</sub>): Uganda and Kenya have equal levels of global social connectedness.
- Alternative hypothesis (H<sub>1</sub>): Uganda and Kenya have different levels of global social connectedness.

The analysis therefore begins by examining their positions within the African network and then tests whether the observed differences extend to their global connections.


## Research Questions

1. How important is Uganda and Kenya in the African social network as measured by the Facebook Social Connectedness Index?
2. Are Ugandans more socially connected than Kenyans in the global network?

## Dataset

**Facebook Social Connectedness Index (SCI)** was published by Meta Research(AI for Good) and distributed via the Humanitarian Data Exchange (HDX). 
It can be found at https://data.humdata.org/dataset/social-connectedness-index. The country.zip dataset was used, it is included in this repo and can be downloaded here: [country.csv](./data/country.csv)
The dataset contains pairwise SCI scores between countries worldwide. The SCI between two countries is defined as:

$$SCI_{i,j} = \frac{\text{FBfriendships}_{i,j}}{\text{FBusers}_i \times \text{FBusers}_j}$$

FB stands for Facebook.

A higher score means people in those two countries are disproportionately likely to be Facebook friends.

## Analysis

The project applies two (2) techniques from the course:

| Question | Technique | Lesson |
|------|-----------|--------|
| 1 | PageRank (iterative method) | Lesson 4 ([link](https://kujenga.readthedocs.io/en/latest/gallery/lesson4/plot_influencer.html?authuser=0)) |
| 2 | Two-sample t-test | Lesson 3 ([link](https://kujenga.readthedocs.io/en/latest/gallery/lesson3/plot_runners.html?authuser=0)) |

### Question 1 (using PageRank algorithm)
The SCI dataset is modelled as a weighted directed graph where countries are nodes and SCI scores are edge weights. 
The PageRank algorithm (damping factor $d=0.85$,  iterative method) is implemented to rank Uganda's and Kenya's importance in the African friendship network accounting not just for how many connections Uganda/Kenya has, but how important those connected countries are.

> **Result:**
> The PageRank analysis shows that Kenya occupies a more important position than Uganda within the African social network.
> Kenya ranks 18th out of 52 countries, compared with Uganda at 46th.
> Therefore, although both countries participate in the wider African network, Kenya is more central according to the PageRank measure used in this study.

### Question 2 (using t-test)
Uganda's and Kenya's log-SCI distributions (over common partner countries) are compared using a two-sided, two-sample t-test to determine whether the difference in mean social connectedness is statistically significant.

- $H_0: μ_{UG} = μ_{KE}$
- $H_1: μ_{UG} ≠ μ_{KE}$

> **Result:**
> The t-test produced a p-value of 0.115926.
> Since this is greater than the significance level of 0.05, I fail to reject the null hypothesis.
> The available SCI data therefore do not provide sufficient evidence that Uganda and Kenya differ significantly in their global social connectedness.

## Key Finding

Despite Kenya's greater economic integration in East Africa, the t-test finds no statistically significant difference between Uganda's and Kenya's global social connectedness ($p ≥ 0.05$). The plot below confirms the t-test result.

![](./media/kde-of-sci-scores.png)

This suggests that geographic proximity and shared migration corridors matter more than economic size in shaping cross-border friendship networks.

## How to Run

- Run online: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/keyxyz/social-fabric-of-africa/blob/main/notebooks/sci-for-african-countries.ipynb)
- Run locally:

    ```bash
    # clone repository
    git clone https://github.com/keyxyz/social-fabric-of-africa.git
    cd social-fabric-of-africa

    # create virtual environment
    python -m venv venv
    source venv/bin/activate
    # for windows
    # source venv/Scripts/Activate.bat 

    # install dependencies
    pip install jupyter pandas numpy matplotlib scipy networkx

    # run
    jupyter lab
    ```

## Limitations

- SCI is based on Facebook users only and so populations without internet access are underrepresented which disproportionately affects African countries.
- A null result in the t-test means we cannot detect a difference, not that no difference exists.

## Conclusion

This study compared Uganda and Kenya using the Social Connectedness Index to examine their positions within the African social network and their global social connectedness. 
The PageRank analysis showed that Kenya ranked higher than Uganda, at 18th and 46th respectively, indicating that Kenya occupies a more central position in the African network. 
However, the statistical test produced a p-value of `0.115926`, which is greater than the `0.05` significance level. 
Therefore, _the null hypothesis is not rejected_, meaning the analysis does not provide sufficient evidence of a statistically significant difference in the global social connectedness of Uganda and Kenya. 
Overall, the findings show that differences in network position do not necessarily imply significant differences in overall social connectedness.


## References

- Bailey, M. et al. (2018). *The Social Connectedness Index.* Meta Research.
- Facebook Social Connectedness Index dataset via HDX: https://data.humdata.org/dataset/social-connectedness-index
- Page, L. et al. (1999). *The PageRank Citation Ranking: Bringing Order to the Web.* Stanford InfoLab.
