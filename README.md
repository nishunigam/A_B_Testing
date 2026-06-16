# A/B Testing

## What is A/B testing?
A/B testing is a way to compare two versions of a single variable , typically by testing a subject’s response to variant A against variant B , and determining which of the two variants is more effective.

Suppose an online learning platform wants you to test whether they should change the web page’s button size to increase the number of users.

<img width="919" height="544" alt="image" src="https://github.com/user-attachments/assets/322db5d6-1df8-435e-a9b3-b2d7426079fb" />

we have:

**Single variable:** "Join Now " button size on a webpage 

**Variant A:** 4 x 3 button size 

**Variant B:** 16 x 9 button size 

**Subject’s response:** click-through probability changes 

**Goal:** find out which option has a higher click-through probability

## When and when not to use A/B Testing

A/B testing has many Use Cases, including:

<ins>UI changes, recommendations, ranking changes, implicit changes such as loading time, etc.</ins>

However, there are also cases it is Not So Useful:

**Missing items** For our online course website example: if there are any courses we didn’t offer, but the users are looking for, A/B testing cannot tell.

**New experiences** Introducing new experiences such as VIP services can be troublesome because:

  - a) The baseline of comparison is not clear

  - b) The time needed for users to adapt to new experiments can be quite costly, as there might be some psychological influences on users:

      - **Change Aversion:** when faced with a new interface or changed functionality, users often experience anxiety and confusion, resulting in a short-term negative effect.

      - **Novelty Effect:** when new techs came out, users will often have increased interests so that the performance will improve initially, but it’s not because of any actual improvement.

 ## What are the Steps of A/B Testing?

 There are 5 main steps for A/B Testing:

 1. **Make a hypothesis about the change:** The first step is exactly what we did in the example above. i.e., We assume that changing the size of the ‘Join Now’ button from 4×3 to 16×9 will affect the number of students enrolled in our online course.

2. **Choose the metrics:** E.g. We want more students to move from the course menu page to a specific course page, so we choose the ‘click-through probability’ as our metric.

3. **Design the experiment setups:** (including the unit of diversion, population, size, and duration), and carry out the test.

4. **Analyse the results:** Calculate the margin based on the confidence interval, and decide whether it satisfies the practical significance requirements.

5. **Make a decision:** Communicate the results and risks with stakeholders.

### Step 2. Choose the Right Metrics

After we set up our goals in step 1, we need to choose the correct metrics to convert the goals to concrete measurements such as click-through probability. It can be **single or multiple** metrics depending on the business needs. If you chose multiple metrics, one way is to combine them with weights to form an **overall evaluation criterion (OEC).** The steps mentioned in this course are:

**1. Invariant (Sanity) Check** Before choosing the measurement metrics that will be affected by the variants, we need to make sure invariants are controlled. For example, do you have the same number of users across the two groups **(population sizing)?** Do they have **comparable distributions** across countries, languages? Ideally, we should also assign the two groups the same **number of trials.**

**2. Determine High-level Business Metrics** This usually involves discussing with domain experts to determine the best practice, such as revenues, market shares, etc. In our online learning case, click-through probability makes more business sense.

**3. Expand to More Detailed Metrics** First of all, we could list the basic **customer funnel** and expand it with more details to better understand the data we need to collect for the metrics. In this case, we need to capture the number of unique users that moves from "exploring the site" to "create an account."

![Customer Funnel of the Online Course Example](<img width="643" height="383" alt="image" src="https://github.com/user-attachments/assets/e2acd49b-423e-4433-b062-7930a14300c4" />)

Then we determine how to **summarise the metrics.** In general, there are 4 ways to summarise the metrics:

  - **Sums and counts,** e.g., Total visits to the home page
    
  - **Distributional metrics,** e.g., Average visits to the home page per day. Aggregations such as mean, median, 25th, 75th percentile, etc.

  - **Probabilities and rates,** e.g. Click-through rates or probabilities Rates: usually used to determine whether this change is easy to find Probabilities: determine whether users like this change

  - **Ratios** eg. Pr(revenue-generating click)/ Pr(total clicks) Any two numbers divided by each other

To choose between these 4 methods, we usually look at:

   - **Distribution of the metrics:** Plot a histogram of past data: if it is normal shaped distribution: choose mean or median if it is one-sided distribution: choose 25th, 75th… percentile

  - **Sensitivity and robustness Sensitivity:** the metrics respond well to **relevant** changes (e.g., button size) **Robustness:** when **irrelevant** changes (e.g., site loading time) happen, the metrics do not change a lot We usually use **A/A Experiments** to test them out. For example, when we use the same setup of a button to test users with different loading times, the click-through probability shouldn’t vary too much (robustness). However, if we use different button sizes, the click-through probability should change accordingly (sensitivity). When new experiments are too costly, we could also do a **Retrospective Analysis** by looking at past data to test out similar scenarios.

### Step 3. Design the Experiment Setups
So far we know what to test on, but before we carry out the test, there are still 4 attributes need to be designed: **Unit of Diversion, Population, Size, and Time.**

**1. Unit of Diversion (Proxies of Users)**

Remember in our online course example, we want to collect the number of unique users that moves from "exploring the site" to "create an account"? So what can be considered a "unique user", or the **unit to run the test**? This is the question that the unit of diversion answers. The commonly used units include:

**User ID, Cookies, Events such as page view, Device ID, IP address**

To determine the best unit, we need to look at:

  - **User experience consistency** Since we don’t want the same person to see different experiment groups at different times, we need to choose the unit that can reduce this effect and get more accurate data at the same time. For example, if we choose cookies as the unit of diversion when users switch to another browser, they may be assigned to a different group.

  - **Variability** We also need to look at the distributions of our metrics to make sure they don’t vary too much so that the practical significance level is realistic for the metrics we choose. For some complicated metrics, the empirical variability can be very different from the analytical one. It usually happens when we observe weird distributions of our metrics or when the unit of analysis (i.e., the denominator of your analysis metrics) is different from the unit of diversion (e.g., using the user id as a unit of diversion but the page view as the unit of analysis). In such cases, we need to use the empirical variability deducted from the A/A experiment.

  - **Ethical issues** Security and confidentiality issues; Whether informed consent is feasible.

**2. Population (Target Users)**

Sometimes we want to target the changes to specific user groups. This is called a **cohort.** For example, if we change the English text prompt of a button, we may only want to test the results on English speaking users.

Note that limiting the population to a cohort may need a longer time to collect sufficient data. So unless we want to increase user stability or reduce the learning effect, using a cohort is unnecessary.

**3. Size**

The questions we need to answer regarding the size include: How many tests do we need to get statistically significant results? How do we reduce the number of tests to save time? These are the 4 parameters that will affect the sample size:

![Parameters that Affects the Sample Size](<img width="557" height="394" alt="image" src="https://github.com/user-attachments/assets/18223115-4629-4ec9-a8ec-d00debff2d6a" />)

And the specific numbers can be calculated [using this calculator](https://www.evanmiller.org/ab-testing/sample-size.html).

**4. Time**
The last parameter to consider is time, which includes:

  - **When to run the test**Many businesses have seasonal effects. If our tests happen to be on holidays or back to school days, the results may not be accurate. So if possible, it’s better to test the results in a comparable time.
    
  - **Duration** As there will be novelty effect and change aversion to a new version of a product, we need to give the users some time to get used to the changes to stabilize the result.

  - **The fraction of traffic** We may have the intuition that if the experiment runs on all the target users, the time needed to collect a sufficient amount of data would be much less. But why the common practice is to run the experiment on a **small portion of the traffic instead?** This is because we are unsure if there are risks in the test version or whether it will harm the user experience. For example, if we are testing a new version of a database, we don’t want it to fail pervasively. By doing so, we could also reduce the effect of variabilities, such as holidays or weekends. Not to mention that the learning effect takes time for users to react normally.

### Step 4. Analyse the Results
Suppose that we have already run the experiment and collected a sufficient amount of data. Shall we move on to analysing the results directly? Not quite, we still need to do another sanity check to ensure the experiment is conducted properly.

**1. Sanity Check**
We have already know the invariants when choosing our metrics. Now we need to check that they actually didn’t change in the experiment. Let’s look at an example:

Say we’ve collected 65554 samples in the "4 X 3" button size group and 61818 in the "16 X 9" group. We want to know whether the number of samples collected in these two groups are roughly the same with 95% confidence.

We could use the formula below for sanity check:
<img width="543" height="161" alt="image" src="https://github.com/user-attachments/assets/abe8b5aa-78af-4c6b-9b90-7c5d70407670" />

1) Compute the standard error of binomial with probability 0.5 of success 2) Lookup Z score of 95% and calculate the margin of error 3) Compute the confidence interval around 0.5 4) Check whether the observed probability is within the confidence interval
<img width="785" height="216" alt="image" src="https://github.com/user-attachments/assets/7c249257-6ab8-4716-802e-c006111f6b39" />

The observed probability is not within the 95% confidence interval in the example above, so something about the setup isn’t correct.

#### So what to do if our sanity check went wrong?
Do not proceed, go straight to analysing why it fails.


First, we could look at the data in a **smaller group,** eg. day by day to find out which part went wrong. If it was technical reasons, we should debug with the engineers.

To prevent the sanity check from failing, we could also add a **pre/post period A/A experiment.** The pre-period test is what we mentioned in "choosing the metrics", while the post-period test is usually used to measure whether learning effect happened in our experiment.

If sanity check only failed in the pre-period, check the experiment set up, infrastructures or things along those lines. If it only failed in the experiment itself, then it’s the data capture issue.

**2. Calculate the statistical significance**
After the sanity check, we finally reach the most exciting part! We can now put together all the hard works and make a decision! In this step, we need to determine if the change is statistically significant, together with the magnitude and direction of the change. For single and multiple metrics, we usually use different strategies.

##### Single Metric

**Hypothesis test** and **sign test** are commonly used to calculate the statistical significance for a single metric. Let’s see the examples：

**Hypothesis test:** Suppose we have the following data and parameters that already passed the sanity check:
<img width="516" height="160" alt="image" src="https://github.com/user-attachments/assets/478bc992-9f6d-402d-8dd1-15ed40bae96a" />

Unlike what we’ve done in the sanity check, we use the pooled probability (overall probability) as the centre of the confidence interval for a better estimation than 0.5 this time. The standard error should also be pooled:
<img width="572" height="71" alt="image" src="https://github.com/user-attachments/assets/f9414121-83f4-4f47-8d9e-563f58c8207e" />

Following the same steps in the sanity check, we could get the result:
<img width="639" height="144" alt="image" src="https://github.com/user-attachments/assets/dd72ce30-3dd7-4826-a8db-1331522e4112" />

Since the lower boundary of the confidence interval is higher than the minimum practical significance level, it is safe to recommend a launch of the experiment version.

If the practical significance level (dₘᵢₙ) falls on a different part of the confidence interval, we could reference this graph:

<img width="1024" height="904" alt="image" src="https://github.com/user-attachments/assets/8356db53-8c33-4db5-ba59-a1f86515fd8d" />
![Confidence Interval VS Practical Significance Level

**Sign Test:** Suppose when we segment the data into different days, 9 out of 14 days the control group has a higher click-through probability.

If there’s no difference between the two groups, the hypothetical probability of "success" should be 0.5. We could then [use this calculator](https://www.graphpad.com/quickcalcs/binomial1/) to get the two-sided P-value. We could see that the two-tail P-value is 0.424, which is much larger than 0.05 for a 95% confidence interval. So the sign test suggests there’s no statistically significant difference.

#### **If the tests do not agree with each other…**
We should break the data down into subgroups to see which part has more effect. You may also encounter the Simpson’s paradox in such cases. A very famous example is the UC Berkeley gender bias.


**Simpson’s Paradox** is a statistical phenomenon that a trend appears in the combined data, but disappears or reverses when the data are partitioned into several different groups.

<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/6d5499ba-7f25-4390-a70c-a8ece2caaf84" />
<em>"Simpsons Paradox Animation" by Pace~svwiki licensed under CC BY-SA 4.0</em>

#### Multiple Metrics
One key difference between single and multiple metrics is that:

The more metrics you test, the more likely you see statistically significant results by chance – Multiple Comparison Controversy


This is because the probability of **false-positives at least occur once** would be higher.

Assume we have 3 metrics all with a false-positive probability of 5%, the chance of having at least 1 statistically significant results is 1–0.95³=0.143. When we have 20 metrics, the probability becomes 1–0.95²⁰=0.642.

Luckily, it is **not repeatable.** If we do the test again or segment it into small groups, it should disappear.

We could also use these techniques to resolve the multiple comparison issue:

#### How to resolve multiple comparison controversy?

The general solution is to use a **higher confidence interval**. This can be achieved by:

  a) Assuming independence, and **set only the overall alpha** Then we use:αᵒᵛᵉʳᵃˡˡ = 1-(1 – αᶦⁿᵈᶦᵛᶦᵈᵘᵃˡ) ⁿ to calculate individual α.

  b) **Bonferroni Correction** This method has no assumptions. It calculates the individual α by αᶦⁿᵈᶦᵛᶦᵈᵘᵃˡ = αᵒᵛᵉʳᵃˡˡ/number of metrics. Note that this is a relatively conservative method, you may miss some valuable observations.

  c) **Familywise Error Rate** The FER only controls the probability that any metric shows a false positive.

  d) **Control False Discovery Rate** In this case, we allow a high probability of false positive, as long as there isn’t too many. Note that FDR should be used when the number of metrics is very large, usually hundreds.

### Step 5. It’s All about Decisions

Up until now, we’ve already calculated the statistical significance and confidence interval with all the cautions. Are we good to bring up the recommendations?

## Things to consider when making decisions

* Is it statistically and practically significant?
+ Do you understand the change?
- For multiple metrics, do they move in the same direction?
* What has the change done to the user experience?
+ Is it worth it?

## Problems may occur when launching
Always do a ramp-up when lauching a change, that’s what we do for all the launches at Google.


Real word data is nasty, so do the test. Even if the test is statistically significant initially, the **effect can be flattened when you ramp up the change** (i.e. gradually increase the percentage of users to the new version). This is mainly because:

  - **Event or seasonal driven impact:** We could holdback (When the changes are not applied to a small number of users, we should see the reverse effect in this group), **cohort analysis, or pre/post period A/A experiment** to test the issue.
    
  - **The results may not be repeatable:** Sometimes our changes will only be effective to 30% of users or have a positive effect on 30% users but negatively affect 70% users. We could do a ramp-up launch to test out this issue.
    
  - **Business effects:** We may also find companies call off the launching when the engineering, or opportunity cost is relatively high, or when there’s customer support or sales issue.

## A Final Note: Ethical Issues

### Risks
The risks the participants are exposed to should not exceed the minimal risk, i.e., the probability and magnitude of harm a participant would encounter in normal daily life. If the risk exceeds minimal risk, informed consent is required.

### Benefits
What benefits might the outcome of the study be?

### Choice
What other choice does the participant have? For example, when testing out new drugs for cancer, the other choice most participants have is death, so that the risk for participants is quite high.

### Privacy (Data Sensitivity)
What expectations of privacy and confidentiality do participants have? Note that the timestamps are considered personally identifiable since they could contain enough information to link the data to a person. This means that any sensitive data, such as health conditions with timestamps, should be considered sensitive.
