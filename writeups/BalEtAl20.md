# Towards causal benchmarking of bias in face analysis algorithms

Guha Balakrishnan, Yuanjun Xiong, Wei Xia, Pietro Perona. [Towards causal benchmarking of bias in face analysis algorithms.](https://arxiv.org/abs/2007.06570) ECCV 2020.

## Abstract
- observational datasets attribute algorithmic bias to dataset bias
- develop a method for measuring algorithmic bias by manipulating the variables of interest to find casual links (basically a different benchmark)
    - generate synthetic datasets
    - use humans!
- compare this method to an observational one

## Intro
- *observational* test set: based from *the wild*, and labeled with attributes like gender, age. so the distribution of these things are sampeld from environment
    - but correlation != causation - just because errors bad on this test set for a certain attribute doesnt mean its *because* of that attribute
        - e.g. PPB dataset, all women have long hair
- *experimental method* : manipulate variables of interest
(MC: lol explaining the scientific method... kinda rude...)
- generate test images synthetically, create transects (grids of images), which is a more balanced dataset, and leads to diff conclusions

## Related Work
- gender shades [12] should be "treated with caution"

## Approach
- assume the system is fixed, measure bias in pre-trained algos
- develop experimental method where we can study any attribute QQ why? it seems weird to try to genrealize across attributes that are so different.

- label their generated dataset using human annotators as ground truth QQ is it right to use gender perception at all ? ?

### QQ generative methods can also be biased? like figure 3 1d transects, some of those look unrealistic, like super bad photoshop of dark skin
- partial A: use human annotators to prune the data

- use stylegan2, which is biased toward generating caucasian-y faces. used human annotations to sample toward parts of latent space with more diversity

#### generation of several attributes:
- project z onto intersection of K hyperplanes
- move in z space

- orthogonalize the hyperplanes, or else attributes (hair length and gender) will influence one another

- estimate *average treatment effect* E1 - E0
- covariate adjustment approach to minimize confounding variables: predict error e^i from one-hot binary covariate vector x^i 

- get human annotations from mturk, remove fake images
- Figure 6: MC makeup guidelines seem extremely vague, why use Regular as an option for facial hair if trying to separate from gender? why not use length?

- Figure 9: glasses generated ?


> The wild-collected datasets contain significant imbalances across gender, particularly with hair length.

but this is representative of population? why do we want to minimize this correlation in figure 12?

> All classifiers perform significantly worse on dark-skinned females.

> There is no consistent transect error pattern in skin tone: within homogeneous groups changing skin tone does not seem to affect the performance of either algorithm. For example, females with long hair see no significant difference in classification error between light vs. dark skin. Looking at PPB alone, we could not make this observation, since skin tone is so strongly correlated with hair length.

MC this is very misleading from the abstract... the conclusion that skin tone has no effect is based on analysis where only skin tone is taken into account. this paper doesnt seem to present the issue that dark-skinned female is classified poorly as an issue.

Figure 13:
- MC: errors are much higher on all female/short hair.  no difference b/w female/short hair/light skin vs. female/short hair/dark skin. this still an issue of skin color because dark skin female short hair, much more common in the real world than light skin female short hair, assuming that PPB is representative of *the wild*. so we should still pay more attention to these errors, because they reflect systemic issues
- QQ Errors are generally higher on synthetic dataset though?

## Regression
- calculate casual effects, predict error conditioned on all attributes

- MC seems sketchy to draw conclusions...

Figure 15:
- skin tone has no effect by itself

- independence assumption is bad.

- QQ why focus on gender classifcation? why do we want to classify people as female or male?


## Limitations

> our method tends to add earrings when transitioning
from dark-skinned men to dark-skinned women, a cue that a gender classifier might use to perform disproportionately
well on the latter group. Because we did not annotate this attribute, it is hidden to our analysis

> our method often adds facial hair to male faces when
increasing hair length

## QQ
-  If youre making something at `industry grade`, what checks are in place to make sure that youre accounting for all these variables? Who is keeping you accountable?
- how do u explain the results on the observational dataset then?
- basically they created a dataset where this bias doesnt exist, and then say lets use this dataset to prove that there is no bias.
- intersectionality is important!
- why try to make statements based on your dataset when it has so many limitations?