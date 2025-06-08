# Problem 1
# Problem 1: Exploring the Central Limit Theorem (CLT) Through Simulations

## 📌 Motivation

The **Central Limit Theorem (CLT)** is a foundational result in probability and statistics. It asserts:

> Given a population with any distribution that has a finite mean $\mu$ and finite standard deviation $\sigma$, the distribution of the sample mean $\bar{X}$ will tend to be approximately normal as the sample size $n$ increases.

In symbols:

$$
\bar{X} \sim \mathcal{N}\left(\mu, \frac{\sigma^2}{n}\right) \quad \text{as } n \rightarrow \infty
$$

This result enables statisticians to apply inferential techniques even when the underlying population distribution is not normal.

---

## 🎯 Objectives

- Simulate samples from various population distributions.
- Visualize the sample mean distributions.
- Observe convergence to the normal distribution.
- Discuss the effect of sample size and population variance.
- Reflect on real-world implications of CLT.

---

## 1. Simulating Sampling Distributions

We consider three population types:

- **Uniform distribution**: $X \sim \mathcal{U}(a, b)$
- **Exponential distribution**: $X \sim \text{Exp}(\lambda)$
- **Binomial distribution**: $X \sim \text{Binomial}(n, p)$

Each distribution generates a large population dataset (e.g., 100,000 values) for sampling.

---

## 2. Sampling and Visualization

We take samples of various sizes:

- Sample sizes: $n = 5, 10, 30, 50$
- For each sample size:
  - Draw 1000 samples from the population
  - Compute the sample mean $\bar{X}$
  - Plot the histogram of sample means

As $n$ increases:

- Sample mean distribution becomes smoother
- Shape becomes increasingly bell-curved (i.e., normal)
- Extreme skew or kurtosis in the population diminishes

---

## 3. Parameter Exploration

### 🔍 Distribution Shape

- Uniform: Converges quickly to normal due to symmetry
- Exponential: Starts skewed, but normality emerges with larger $n$
- Binomial: Discrete but approximates normal if $n$ is large and $p$ not extreme

### 🔍 Sample Size Impact

- The variance of the sampling distribution decreases with $n$
- The formula for the variance of sample mean:

$$
\text{Var}(\bar{X}) = \frac{\sigma^2}{n}
$$

Hence, larger $n$ reduces the spread of the sample mean histogram.

---

## 4. Practical Applications

- **Parameter Estimation**: Means from samples are used to infer population characteristics
- **Manufacturing**: Control charts based on sampling assume normality
- **Finance**: Return models use CLT to assume average performance is normally distributed
- **Epidemiology**: Average rates (e.g., infection rates) are modeled under CLT assumptions

---

## 📚 Key Definitions

- **Sample Mean**: $\bar{X} = \frac{1}{n} \sum_{i=1}^{n} X_i$
- **Population Mean**: $\mu = \mathbb{E}[X]$
- **Sample Variance**: $s^2 = \frac{1}{n-1} \sum_{i=1}^{n} (X_i - \bar{X})^2$
- **Sampling Distribution**: Distribution of $\bar{X}$ over many samples
- **Normal Distribution**: A symmetric bell-shaped distribution defined by $\mathcal{N}(\mu, \sigma^2)$

---

## 📈 Visual Summary (to be attached)

- Histograms of sample means for each population and $n$
- Normal curves overlayed for comparison
- Convergence clearly visible as $n$ increases

---

## 🧠 Conclusion

- CLT holds regardless of population shape, provided sample size is sufficiently large
- Larger $n$ and smaller $\sigma$ lead to faster convergence
- CLT provides the mathematical foundation for many real-world statistical methods
![1](https://github.com/user-attachments/assets/1ade8248-68ed-4044-9269-674c4b8a457f)
![2](https://github.com/user-attachments/assets/9bd87e44-6824-4bbd-9257-7645422e68b8)
![3](https://github.com/user-attachments/assets/06d1d8ca-a513-41c2-a3e6-86cc63c2e1e3)

 ```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import gaussian_kde

# Stil ayarı
sns.set(style="whitegrid")

# Popülasyonların tanımlanması
uniform_population = np.random.uniform(0, 1, 10000)
exponential_population = np.random.exponential(1, 10000)
binomial_population = np.random.binomial(n=1, p=0.5, size=10000)

# Tüm popülasyonları bir sözlükte tut
populations = {
    'Uniform': uniform_population,
    'Exponential': exponential_population,
    'Binomial': binomial_population
}

# Farklı örneklem büyüklükleri
sample_sizes = [5, 10, 30, 50]

# Tüm popülasyonlar için işlem
for name, population in populations.items():
    plt.figure(figsize=(16, 10))

    for i, size in enumerate(sample_sizes, 1):
        sample_means = []
        for _ in range(1000):
            sample = np.random.choice(population, size=size)
            sample_means.append(np.mean(sample))

        # Alt grafik oluştur
        plt.subplot(2, 2, i)

        # Histogram
        sns.histplot(sample_means, bins=30, color="orchid", stat="frequency", kde=False)

        # KDE (manuel çizim)
        kde = gaussian_kde(sample_means)
        x_vals = np.linspace(min(sample_means), max(sample_means), 200)
        y_vals = kde(x_vals) * len(sample_means) * (max(sample_means) - min(sample_means)) / 30
        plt.plot(x_vals, y_vals, color='darkmagenta', linewidth=2)

        plt.title(f"{name} Distribution - Sample Size {size}")
        plt.xlabel("Sample Mean")
        plt.ylabel("Frequency")

    plt.suptitle(f"Sampling Distribution of the Mean - {name}", fontsize=18)
    plt.tight_layout()
    plt.show()
     ```

## 🔗 References

- Wasserman, L. (2004). *All of Statistics*
- Khan Academy: [Central Limit Theorem](https://www.khanacademy.org/math/statistics-probability)
- [Wikipedia: Central Limit Theorem](https://en.wikipedia.org/wiki/Central_limit_theorem)



