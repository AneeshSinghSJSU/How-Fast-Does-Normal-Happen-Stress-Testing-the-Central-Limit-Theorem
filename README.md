# CLT Monte Carlo Project

**Course:** Math 167R  
**Author:** Aneesh Singh

## Project purpose

This project investigates how the sampling distribution of the sample mean changes as sample size increases. It compares five assigned populations using Monte Carlo simulations, histograms, normal Q–Q plots, and numerical summaries, with attention to the assumptions of the Central Limit Theorem.

## Population analyses

Update the file links below to match the filenames and folders in your repository.

| Population | Assigned parameters | Analysis |
|---|---|---|
| Standard normal | Mean 0; standard deviation 1 | [normal.qmd](normal.qmd) |
| Fair six-sided die | Outcomes 1–6, equally likely | [die.qmd](die.qmd) |
| Exponential | Rate 1 | [exponential.qmd](exponential.qmd) |
| Small binomial | 5 trials; success probability 0.10 | [binomial-small.qmd](binomial-small.qmd) |
| Cauchy | Location 0; scale 1 | [cauchy.qmd](cauchy.qmd) |

## Simulation approach

Each experiment generates repeated samples and records their sample means.

- `n` is the number of observations in one sample.
- `B` is the number of samples generated for each sample size.
- Histograms, Q–Q plots, and numerical summaries provide evidence about the sampling distribution.
- Simulated means and standard errors are compared with theoretical values where those values exist.

**Repetitions per sample size:** 10,000  
**Main random seed:** 9686  
**Alternate seed used for the reproducibility experiment:** 0176

### My definition of approximately normal

An average mean (the mean of the means in the histogram) which differs from the expected mean (0.5) by less than 0.01 meets my criterion for the center. This is an absolute tolerance, and proximity to the theoretical mean alone does not establish a normal distribution.

For the Q-Q plot, I use a normalized RMSE below 0.05. This is the root mean square of the vertical gaps between the Q-Q points and the reference line, divided by the reference line's slope. It measures departures across all points, including the tails; it does not require every individual gap to be below 0.05.

## Executive summary and comparison

| Population | Smallest tested n meeting criteria | Simulated mean | SD of simulated means | Theoretical SE | Normalized Q–Q RMSE | Main observation |
|---|---|---|---|---|---|---|
| Standard normal | 1 | 0.0013 | 1.0040 | 1.0000 | 0.0136 | At n = 1, mean error 0.0013 and normalized Q–Q RMSE 0.0136 meet both cutoffs. |
| Fair six-sided die | 50 | 3.5052 | 0.2428 | 0.2415 | 0.0484 | n = 40 misses the Q–Q cutoff (0.0508); n = 50 passes (0.0484). |
| Exponential | 125 | 0.9996 | 0.0911 | 0.0894 | 0.0475 | n = 100 misses the Q–Q cutoff (0.0560); n = 125 passes (0.0475). |
| Small binomial | 230 | 0.5005 | 0.0442 | 0.0442 | 0.0412 | n = 225 misses the Q–Q cutoff (0.0565); n = 230 passes (0.0412). |
| Cauchy | None meets Q–Q cutoff; values at n = 1000 | 1.4693 | 163.9289 | Undefined | 111.8273 | No tested n passes the Q–Q cutoff. Values here are from n = 1000; theoretical mean and SE are undefined. |

The results clearly demonstrate the impossibility of a universal n value where any n becomes normal. While it might be possible to say that for any whose population has a mean there exists an n such that any is even (such as limit as n approaches infinity), that cannot be applied to every population as Cauchy clearly demonstrates that without a mean the central limit theorem does not apply and it will never reach normality.

The ones which reached normality the fastest were naturally the normal population but also the six sided die, while the exponential and small binomial took the longest (Cauchy won't be counted as it never reached normality). The shapes played a bit part in the ease at which they became normal. The normal population was already normal, the die was evenly spread so it wasn't hard to it to become normal. On the other hand, exponential and binomial were heavily skewed left with large tails to the right which forced massive changes over large amounts of n to resemble a normal distribution. While I did initially assume that the sample size would need to be something like 50 in order to work, it's clear now that because nearly every value must be shifted radically that while it can does confirm the Central Limit Theorem it only does so with large values of n.

As mentioned earlier, I was surprised at the extremity of the values of n required to make exponential and binomial populations normal, but besides that it was for the most part what I expected. There were some severe limitations regarding the experiment however, most notably the definition of normality as using just it's proximity to the expected mean didn't work well for skewed populations. Instead, it's proximity to the median or it's ability to conform to a normal distributions bell curve. Testing only two seeds and the limited amount of n values tested were also limitations of the experiment which could be remedied.

## How to reproduce the analyses

1. Use R and RStudio with Quarto support.
2. Install the R rendering packages if needed. Run this in the R console:

   ```r
   install.packages("rmarkdown")
   ```

   This also installs `knitr`, which is used for the result tables and execution of R code.
3. Download or clone this repository.
4. Open an analysis `.qmd` file in RStudio.
5. Click **Render** to execute its code and generate the HTML report.

## AI assistance record

The conversation record is stored separately in [clt-conversation-transcript.txt](clt-conversation-transcript.txt).

The exported record marks earlier assistant replies that were unavailable.

AI was used throughout this experiment to assist in menial tasks such as copying over given information such as the definition of normality, along with assisting in coding. I did not use AI to come to my conclusions, however I did use to review my work and make sure I was not omitting details which may be important.

