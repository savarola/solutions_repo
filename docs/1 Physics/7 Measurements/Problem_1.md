# Problem 1 – Measuring Earth's Gravitational Acceleration with a Pendulum

---

## 🧠 Theory

The period $T$ of a simple pendulum of length $L$ under gravity $g$ is given by:

$$
T = 2\pi \sqrt{\frac{L}{g}} \quad \Rightarrow \quad g = \frac{4\pi^2 L}{T^2}
$$

To measure $g$, we:
- Measure the length $L$ of the pendulum.
- Measure the time it takes to complete 10 full oscillations.
- Calculate $T$ and then $g$.
- Perform uncertainty propagation to determine $\Delta g$.

---

## 🧪 Equipment

| Equipment          | Description                          |
|--------------------|--------------------------------------|
| String             | Approx. 1 meter                      |
| Small mass         | Keychain, washer, or similar         |
| Stopwatch          | Smartphone or digital timer (0.01 s) |
| Ruler/Measuring Tape | 1 mm resolution                     |

- Length uncertainty: $\Delta L = \frac{1}{2} \cdot \text{resolution} = 0.0005$ m

---

## 🔬 Procedure

1. Set up the pendulum and measure $L$.
2. Displace it by less than $15^\circ$ and release.
3. Record time for 10 oscillations, 10 times.
4. Calculate average, standard deviation, and estimate $g$.

---

## 📊 Data Table

### ⏱️ Timing Measurements for 10 Oscillations

| Trial | $T_{10}$ (s) |
|-------|--------------|
| 1     | 20.01        |
| 2     | 20.14        |
| 3     | 20.06        |
| 4     | 20.03        |
| 5     | 20.11        |
| 6     | 20.07        |
| 7     | 20.12        |
| 8     | 20.05        |
| 9     | 20.09        |
| 10    | 20.08        |

- Mean time $\overline{T_{10}} = 20.076$ s  
- Standard deviation $\sigma_T = 0.0386$ s  
- Uncertainty in mean:

$$
\Delta T_{10} = \frac{\sigma_T}{\sqrt{n}} = 0.0122 \text{ s}
$$

---

## 🔢 Calculations

### 🎯 Period of one oscillation

$$
T = \frac{\overline{T_{10}}}{10} = 2.0076 \text{ s}, \quad \Delta T = \frac{0.0122}{10} = 0.00122 \text{ s}
$$

### 🎯 Gravitational acceleration

$$
g = \frac{4\pi^2 L}{T^2} = \frac{4\pi^2 \cdot 1.000}{(2.0076)^2} \approx 9.812 \, \text{m/s}^2
$$

---

## 📉 Uncertainty Analysis

### 🔧 Propagation of Uncertainties

$$
\frac{\Delta g}{g} = \sqrt{ \left( \frac{\Delta L}{L} \right)^2 + \left( 2 \cdot \frac{\Delta T}{T} \right)^2 }
$$

$$
= \sqrt{ \left( \frac{0.0005}{1.000} \right)^2 + \left( 2 \cdot \frac{0.00122}{2.0076} \right)^2 } \approx 9.95 \times 10^{-4}
$$

$$
\Delta g = g \cdot 9.95 \times 10^{-4} \approx 0.0098 \, \text{m/s}^2
$$

---

## ✅ Final Results

| Quantity       | Value               |
|----------------|---------------------|
| $L$            | 1.000 m             |
| $\Delta L$     | 0.0005 m            |
| $\overline{T_{10}}$ | 20.076 s       |
| $\sigma_T$     | 0.0386 s            |
| $\Delta T_{10}$| 0.0122 s            |
| $T$            | 2.0076 s            |
| $\Delta T$     | 0.00122 s           |
| **$g$**        | **9.812 m/s²**      |
| **$\Delta g$** | **0.0098 m/s²**     |

---

## 💬 Discussion

- **Accuracy**: Our value of $g = 9.812 \pm 0.0098$ m/s² is very close to the standard value $9.81$ m/s².
- **Uncertainty Sources**:
  - Human reaction time (dominant for $\Delta T$).
  - Measurement resolution of tape.
  - Small-angle approximation.
- **Improvements**:
  - Use automated timing.
  - Use higher resolution tools.
  - Repeat more trials for better statistics.

---

## 📎 Conclusion

This experiment effectively demonstrates how basic tools and careful data analysis allow us to estimate a fundamental constant of nature — gravitational acceleration $g$ — with surprisingly high accuracy.

