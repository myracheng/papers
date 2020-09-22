# Gender Shades

Joy Buolamwini, Timnit Gebru. [Gender Shades: Intersectional Accuracy Disparities in Commercial Gender Classification.](http://proceedings.mlr.press/v81/buolamwini18a/buolamwini18a.pdf) FAT 2018. 905 cites.

## abs
- use skin type system to analyze face analysis benchmarks
- new dataset: balanced by gender, skin type
- using commercial gender classification systems, darker skinned female are the most misclassified. lighter skin male = very accurate

## intro
- we need datasets that have these labels, so that we can measure bias

## intersectional evaluation of accuracy
- labeled existing datasets with:darker females, darker males, lighter females, and lighter males 
    - use skin type rather than race bc ppl of same race can look very different
    - default camera settings calibrated to expose lighter skin
- evaluated IJB-A, us govt benchmark, and Adience (released in 2014)

- developed Pilot Parliaments Benchmark: three African countries, three European countries w/ gender parity in their parliaments

- Fitzpatrick classification sksyetm: three / 6 categories are for white

## performance results
- analyzed microsoft, ibm, face++
- better on male than female, lighter than dark.

- could it be because of image quality? or other differences in imaging?
    - South African has higher resolution

- pose, illumination, expression, etc also have effects.
    - but these are relatively constrained, since PPB are all official headshots?


## qq
what about other facial recognition algorithms? is gender classification generalizable? why did they pick this