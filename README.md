# 4R+Σ Instrument: Disturbance Response & Memory

**Author:** Nicholas R Egleton
**Correspondence:** egletonnicholas@gmail.com

This repo implements a 4R+Σ instrument for quantifying how dynamical systems respond to disturbance and remember it.

## Core Idea
D1 = immediate response
D2 = rate of change
D3 = curvature
Σ = integrated memory over time

## Files
- `texture_sweep.py` - Run the full experiment
- `paper.pdf` - Full manuscript

## License
MIT
import numpy as np
import matplotlib.pyplot as plt

# 4R+Σ Texture Sweep
t = np.linspace(0, 10, 1000)
D1 = np.sin(t) * np.exp(-0.1*t)
D2 = np.gradient(D1, t)
D3 = np.gradient(D2, t)
Sigma = np.cumsum(np.abs(D1)) * (t[1]-t[0])

plt.figure(figsize=(10,6))
plt.plot(t, D1, label='D1 Response')
plt.plot(t, D2, label='D2 Rate')
plt.plot(t, D3, label='D3 Curvature')
plt.plot(t, Sigma, label='Σ Memory')
plt.legend()
plt.title('4R+Σ Instrument Output')
plt.xlabel('Time')
plt.savefig('figures/sweep.png')
plt.show()


# A 4R+Σ Instrument for Quantifying Disturbance Response and Memory in Dynamical Systems

**Nicholas R Egleton**  
Correspondence: egletonnicholas@gmail.com  
Date: August 10, 2026

---

## Abstract
We introduce the 4R+Σ instrument, a framework for measuring how dynamical systems respond to disturbance and retain memory of that disturbance over time. The instrument decomposes system behavior into four response components D1-D3 plus an integrated memory term Σ. We demonstrate the method on synthetic texture sweeps and show that Σ captures hysteresis and path-dependence that D1-D3 alone miss. The framework is model-agnostic and can be applied to physical, biological, and AI systems.

**Keywords:** disturbance response, system memory, dynamical systems, 4R+Σ, hysteresis

---

## 1. Introduction
Most analysis of dynamical systems focuses on immediate response to input. But real systems remember. A bridge remembers past loads. A neural network remembers past training. A market remembers past shocks.

The 4R+Σ instrument quantifies both the response and the memory.

- **D1**: Immediate response to disturbance
- **D2**: Rate of change of response  
- **D3**: Curvature / acceleration of response
- **Σ**: Integrated memory, the area under |D1| over time

---

## 2. Methods
Given a time series of system output $x(t)$ under disturbance $u(t)$:

$$D1(t) = x(t) -
