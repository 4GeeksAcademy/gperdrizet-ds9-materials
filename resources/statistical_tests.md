# Statistical tests

The tests listed below cannot be used with nominal data as the dependent variable. Choosing the correct statistical test and plotting data effectively depends on the data's statistical type. See the Wikipedia article [*Statistical data type*](https://en.wikipedia.org/wiki/Statistical_data_type) for more information.

The tests below come in two flavors that differ in assumptions. Parametric tests (t-test, F-test) make assumptions about the population's distribution and parameters, non-parametric tests (Mann-Whitney, Kruskal–Wallis) do not. Parametric vs non-parametric is a useful distinction when thinking about statistical tests and models. See [*Parametric and Nonparametric: Demystifying the Terms*](https://github.com/4GeeksAcademy/gperdrizet-ds9-materials/blob/main/resources/articles/Hoskin_parametric_and%20_nonparametric.pdf).

## 1. Student's t-test

- Use this test for comparing two groups.
- Wikipedia article: [Student's t-test](https://en.wikipedia.org/wiki/Student%27s_t-test)
- SciPy.stats implementation: [ttest_ind()](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html)

**Notes:** Tests wether the difference between two groups is significant or not. Assumes that the data from which the samples were drawn is normally distributed and the samples have the same variance. If this is not true, see the Mann-Whitney U test, below.

## 2. ANOVA (also known as the F-test)

- Use this test for comparing multiple groups.
- Wikipedia article: [F-test](https://en.wikipedia.org/wiki/F-test)
- SciPy.stats implementation: [f_oneway()](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.f_oneway.html)

**Notes:** Tests whether or not one or more of the group means are different from the others. Assumes the data was drawn from a normally distributed population. If this is not true, see the Kruskal–Wallis test, below. Determining which sample(s) is/are different requires further analysis (see [Tukey's range test](https://en.wikipedia.org/wiki/Tukey%27s_range_test)).

## 3. Mann-Whitney U test

- Use this test for comparing two groups that are not normally distributed.
- Wikipedia article: [Mann–Whitney U test](https://en.wikipedia.org/wiki/Mann%E2%80%93Whitney_U_test)
- SciPy.stats implementation: [mannwhitneyu()](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.mannwhitneyu.html)

**Notes:** Uses the rank order of observations to test for difference between two groups. Data must be at least ordinal (larger or smaller has a clear meaning) and assumes that the shapes of the sample distributions are similar. If you decide not to use this test because the sample distributions look very different, you have your answer already. For completeness, maybe see the [Kolmogorov–Smirnov test](https://en.wikipedia.org/wiki/Kolmogorov%E2%80%93Smirnov_test) anyway.

## 4. Kruskal–Wallis test (also known as ANOVA on ranks)

- Use this test for comparing two or more groups that are not normally distributed.
- Wikipedia article: [Kruskal–Wallis test](https://en.wikipedia.org/wiki/Kruskal%E2%80%93Wallis_test)
- SciPy.stats implementation: [kruskal()](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.kruskal.html)

**Notes:** Uses rank order of observations to test whether or not one or more groups is different from the others. Follows the similar assumptions to the Mann-Whitney U test, above.
