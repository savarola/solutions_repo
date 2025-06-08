# Measuring the Acceleration Due to Gravity with a Simple Pendulum

## Objective

To determine the acceleration due to gravity, $g$, using a simple pendulum, and to analyze the uncertainties in the measurements.

---

## Apparatus

- String (length $\approx 1.000$ m)
- Small weight (metal washer, keychain)
- Stopwatch (precision: $0.01$ s)
- Ruler or measuring tape (precision: $1$ mm)

Uncertainty in length:

$$
\Delta L = \frac{1 \, \text{mm}}{2} = 0.0005 \, \text{m}
$$

---

## Procedure

1. Construct a simple pendulum of length $L = 1.000$ m from the suspension point to the center of mass.
2. Displace the pendulum by a small angle ($<15^\circ$) and release it.
3. Use a stopwatch to measure the time taken for 10 complete oscillations.
4. Repeat the measurement 10 times and record the results.
5. Compute the average time, standard deviation, and uncertainty.
6. Determine the period $T$ and calculate $g$ using the standard formula.

---

## Observations

### Time for 10 Oscillations

| Trial | Time (s) |
|-------|----------|
| 1     | 15.59    |
| 2     | 15.53    |
| 3     | 15.60    |
| 4     | 15.69    |
| 5     | 15.52    |
| 6     | 15.52    |
| 7     | 15.70    |
| 8     | 15.62    |
| 9     | 15.49    |
| 10    | 15.58    |

Average time:

$$
\overline{T_{10}} = 15.584 \, \text{s}
$$

Standard deviation:

$$
\sigma_T = 0.0674 \, \text{s}
$$

Uncertainty in mean time:

$$
\Delta T_{10} = \frac{\sigma_T}{\sqrt{10}} = 0.0213 \, \text{s}
$$

![download](https://github.com/user-attachments/assets/31c3ade5-6af5-411f-a655-34aad9e25dcb)

```python
import matplotlib.pyplot as plt
import numpy as np

# Örnek veriler
times = [15.59, 15.53, 15.60, 15.69, 15.52, 15.52, 15.70, 15.62, 15.49, 15.58]
trials = list(range(1, len(times)+1))

# Ortalama ve standart sapma
mean_time = np.mean(times)
std_dev = np.std(times)

# Grafik çizimi
plt.figure(figsize=(10, 5))
plt.plot(trials, times, marker='o', color='royalblue', linewidth=2, label='Time for 10 oscillations')
plt.axhline(mean_time, color='green', linestyle='--', linewidth=1.5, label=f'Mean = {mean_time:.2f}s')
plt.fill_between(trials, mean_time - std_dev, mean_time + std_dev, color='lightblue', alpha=0.4, label='±1 SD')

# Etiketler ve başlık
plt.title("Measured Time for 10 Oscillations")
plt.xlabel("Trial")
plt.ylabel("Time (s)")
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```
---

## Calculations

### Time Period of One Oscillation

$$
T = \frac{\overline{T_{10}}}{10} = \frac{15.584}{10} = 1.5584 \, \text{s}
$$

$$
\Delta T = \frac{\Delta T_{10}}{10} = \frac{0.0213}{10} = 0.00213 \, \text{s}
$$

---

### Acceleration Due to Gravity

\[
g = \frac{4 \pi^2 L}{T^2}
= \frac{4 \cdot \pi^2 \cdot 1.000}{(1.5584)^2}
= \frac{39.4784}{2.4296}
= 16.24 \, \text{m/s}^2
\]

---

### Uncertainty in $g$

\[
\frac{\Delta g}{g} = \sqrt{
\left( \frac{\Delta L}{L} \right)^2
+
\left( 2 \cdot \frac{\Delta T}{T} \right)^2
}
= \sqrt{
(0.0005)^2 + (2 \cdot 0.00213 / 1.5584)^2
}
= 0.0027
\]

\[
\Delta g = g \cdot \frac{\Delta g}{g}
= 16.24 \cdot 0.0027
= 0.044 \, \text{m/s}^2
\]

---

## Final Result

\[
g = 16.24 \pm 0.044 \, \text{m/s}^2
\]

---

## Discussion

- The calculated value of $g$ is higher than the standard value $9.81 \, \text{m/s}^2$.
- Potential reasons:
  - Human reaction delay using a stopwatch
  - Miscounting of oscillations
  - Slight deviation from small angle assumption
- Major uncertainty source: $\Delta T$
- Accuracy can be improved by:
  - Increasing pendulum length
  - Timing more oscillations (e.g., 20)
  - Using electronic timing methods

---

## Conclusion

The experiment illustrates how $g$ can be determined using a simple pendulum and basic equipment. Proper technique and uncertainty analysis are essential for obtaining reliable and accurate results.
