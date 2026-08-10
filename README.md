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
