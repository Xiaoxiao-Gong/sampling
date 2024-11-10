# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Xiaoxiao Gong

```
Please write your explanation here...
task 1: Identify all stages at which sampling is occurring in the model. 
my answer: 
From the sampling frame perspective, this code creates a sample of 1000 people, where 200 attend weddings and 800 attend brunches. Here, "wedding" and "brunch" are the "events" in the code.

From the sampling procedure perspective, for selecting the infected individuals, the code uses the function np.random.choice(), which is a simple random sampling method. By defining ATTACK_RATE = 0.10, 10% of individuals are randomly chosen, assuming that 10% of the 1000 people will be infected. This type of sampling is unbiased. Similar to the blog post, different scenarios are defined, but no scenario is set to have a higher risk of infection.

For tracing the infected individuals, the code uses probability sampling. By defining TRACE_SUCCESS = 0.20, each infected individual has a 20% chance of being successfully traced. Compared to the blog post, this step optimizes the process, since it reflects the real-world situation where, due to certain reasons, it is not possible to trace all infected individuals, and data may be missing randomly.

In the secondary tracing step, SECONDARY_TRACE_THRESHOLD = 2 is defined to indicate that if the number of successfully traced infected individuals in an event reaches 2, then secondary tracing will be conducted for everyone in that event. This is a form of conditional sampling. This step corresponds to what the blog post mentioned: events like weddings, which are more organized, are easier to trace. This makes the analysis mistakenly conclude that weddings are more likely to spread infections. The conditional sampling here simulates this overemphasis, reflecting the bias in the analysis.


task 2:compare the results to the graphs
my answer:
The overall trend of the graphs is consistent, the infection proportion obtained through contact tracing (in red) is usually higher than the actual infection proportion (in blue), especially in easily traceable settings like weddings. This indicates that the contact tracing data is biased and tends to overestimate infections attributed to weddings.

However, there are some differences in the specific shape and peak positions of the graphs. In the blog, the blue bars are concentrated around 20%, while the red bars are around 40%. In my generated graph, the difference between the two is not as pronounced.



task 3:Modify the number of repetitions in the simulation to 1000.
my answer:
After changing the number of simulations to 1000, the output became much less stable. The peak positions of the histogram changed each time I ran it, which shows the results were less consistent because of the smaller sample size. So, the reproducibility wasn't great



task 4: Alter the code so that it is reproducible

What I did was reduce the number of simulations and set a random seed. This prevents the previous issue where the peak positions of the histogram varied due to different random numbers, ensuring the reproducibility of the results. Additionally, the histogram output for 1000 simulations showed more variability compared to 50000 simulations, with greater randomness. Overall, the trend in the results is similar to before, with the red bars (traced infection proportion) being higher than the blue bars (actual infection proportion), indicating that the infection rate for weddings is overestimated during tracing.
```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
