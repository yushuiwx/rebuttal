# Additional Ablation Studies
We conducted additional ablation studies to analyze the effects of RE:

* **The number of experts $N$ on Charades-UA and TACoS-UA**

We supplement ablation study for $N$ experts on Charades-UA and TACoS-UA with CMF+RE. The experimental results are presented in the table below:

On Charades-UA:

| N     | R@0.5     | R@0.7     | mIoU      |
| :---- | :--- | :--- | :--- |
| N = 2 | 57.77     | 34.64     | 51.85     |
| N = 4 | **59.84** | **35.97** | 51.64     |
| N = 6 | 58.98     | 35.38     | 50.59     |
| N = 8 | 58.74     | 35.57     | **52.15** |

On TACoS-UA:

| N     | R@0.5     | R@0.7     | mIoU      |
| :---- | :---- | :---- | :--- |
| N = 2 | 35.57     | 20.37     | 35.16     |
| N = 4 | 39.59     | 24.39     | 36.23     |
| N = 6 | **40.36** | **25.62** | **37.81** |
| N = 8 | 38.56     | 24.62     | 36.90     |

* **Top-K selection**

Reviewer A3oF suggested that we should experiment with Top-k selection—specifically, selecting the top k results from the heads based on the router's probability values and using weighted aggregation to derive the final outcome—to enhance our routing. This suggestion is interesting and meaningful, as Top-k selection is widely used in various prevalent network architectures, such as Mixture of Experts (MoE). Consequently, we conducted experiments with Top-2 and Top-3 selections. The results are presented at following:

| Method         | R@0.5     | R@0.7     | mIoU      |
| :--- | :--- | :--- | :--- |
| CMF            | 20.85     | 7.09      | 23.54     |
| CMF + RE       | 21.78     | 8.71      | 24.15     |
| CMF + RE Top-2 | **22.49** | **10.51** | **24.26** |
| CMF + RE Top-3 | 21.51     | 9.85      | 24.11     |

We find that (1) **Both Top-2 and Top-3 selection can further enhance the performance of RE.** (2) **The performance with Top-3 selection decreased compared to Top-2**, and we speculate that this may be due to our RE utilizing only four heads. When the results from a majority of the heads are considered (for instance, three out of four in Top-3), and given that different heads capture different distributions, forcibly combining more distribution results may lead to a reduction in model performance. This suggests that Top-2 may be the most suitable selection strategy for our RE.
