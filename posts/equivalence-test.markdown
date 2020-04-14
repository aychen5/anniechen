---
layout: default
title:  Equivalence Testing
parent: Musings
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


Equivalence Testing

The routine "balance check" involves testing the null hypothesis that the treated and control groups are not significantly different from one another. Although the (conditional) ignorability assumption in causal inference is not directly testable -- the distribution of potential outcomes is unobservable; hence, "assumption" -- balance on the pre-treatment covariates provides evidence that this condition is satisfied. The conventional approach is based on the simple two sample t-test. If the treated sample diverges greatly from the control at some \\(\alpha\\)-level, we reject the null hypothesis defined as similarity of the groups (suggesting a violation of ignorability). Conversely, a failure to reject the null is taken as evidence that ignorability holds. The latter warrants further elaboration.

As you might be aware, the failure to reject the null hypothesis of no difference *does not* mean that we can *accept* that there are no differences. In the frequentist tradition, the null hypothesis is set up as a point estimate. For instance, the mean difference \\(H_0: \mu_1 - \mu_2 = 0\\). If our test does not reject \\(\mu_1 - \mu_2 = 0\\), there is still a range of possible null values and there remains uncertainty about *which* null hypothesis is true. My favourite analogy for this is that rejecting the null is akin to a jury finding a defendant guilty -- there is sufficient evidence for jurors to be reasonably confident in the defendant's culpability. Whereas a non-guilty verdict is comparable to a failure to reject the null hypothesis. This second scenario may arise simply because the data we have falls short, which is to say, it is easy to conflate lack of power for null effects.

Understanding the above is crucial to realising why naive balance tests employing a series of t-tests can be so problematic. And this does not even touch on correction procedures for multiple-testing. In causal inference, when hypothesis testing is set up like so, the null is framed as a claim about the consistency of the data under an assumption of unconfoundedness. The alternative asserts the opposite, the data are inconsistent with unconfoundedness. In other words, covariates with differences in means found to be "statistically significant" are not balanced between treated and untreated groups, and calls into question the exogeneity of the treatment.

As Erin Hartman and Daniel Hildago point out, this backwards logic comes from co-opting a statistical test that is designed to test for *no difference* when we are, in fact, interested in testing for difference. Equivalence testing inverts the null and alternative hypotheses. If we think about it in terms of Type I error, a false positive in the traditional framework is the rejection of a no-difference null hypothesis when there is truly no difference. However, this is misaligned with the kind of Type I error we are typically interested in for the purposes of balance testing, where a false positive would instead be: finding balance in covariates when there is in fact no balance. Under equivalance testing, the Type I error becomes rejecting the null of difference when differences are substantial in actuality. Clearly, it is this kind of Type I error that is consistent with the intuitive understanding of covariate balance. Formally,

$$H_0: \frac{\mu_1 - \mu_2}{\sigma} \geq \epsilon_U ,  \frac{\mu_1 - \mu_2}{\sigma} \leq \epsilon_L$$

Where \(\epsilon_U\) and \(\epsilon_L\) are the upper and lower equivalence bounds. Consider the juxtaposition of a two-sided t-test against two one-sided t-tests (one popular equivalence test) in the graphic below. In TOST, the null of difference is rejected if the p-value is less than $\alpha$ for both one-tailed tests.

An alternative way of thinking about this is using \\([100 \times (1 - 2 \alpha)]\%\\) confidence intervals to determine whether the interval estimate are within an equivalence range.

```r
ggplot(data = data.frame(x = c(-5, 5)), aes(x)) +
  stat_function(fun = dnorm, n = 101,
                args = list(mean = 0, sd = 1)) +
  geom_vline(xintercept = c(-1.96, 1.96), lty = 2, col = "red") +
  stat_function(fun = dnorm,  xlim = c(-5,-1.96), geom = "area", alpha = 0.5) +
  stat_function(fun = dnorm,  xlim = c(1.96, 5), geom = "area", alpha = 0.5) +
  annotate("text", x = c(-2.6, 2.6), y = 0.05, label = "alpha/2", parse = TRUE) +
  annotate("text", x = 0, y = 0.2, label = "Fail to reject null\n of no difference", size = 3) +
  labs(y = "Density", x = "", title = "Test of Difference") +
  theme_bw()
```

<img src="https://aychen5.github.io//anniechen/posts/images/t-test.jpg">


```r
ggplot(data = data.frame(x = c(-5, 5)), aes(x)) +
  stat_function(fun = dnorm, n = 101, args = list(mean = -2, sd = 1)) +
  stat_function(fun = dnorm, n = 101, args = list(mean = 2, sd = 1)) +
  stat_function(fun = dnorm,  args = list(mean = -2, sd = 1),
                xlim = c(-0.5, 5), geom = "area", alpha = 0.5) +
  stat_function(fun = dnorm,  args = list(mean = 2, sd = 1),
                xlim = c(-5, 0.5), geom = "area", alpha = 0.5) +
  geom_vline(xintercept = c(-0.5, 0.5), lty = 2, col = "red") +
  annotate("text", x = 0, y = 0.1, label = "alpha", parse = TRUE) +
  annotate("text", x = 0, y = 0.3, label = "Reject null\n of difference", size = 2.8) +
  labs(y = "Density", x = "", title = "Equivalence Test: Two One-sided T-tests") +
  theme_bw()
```

<img src="https://aychen5.github.io//anniechen/posts/images/tost.jpg">
