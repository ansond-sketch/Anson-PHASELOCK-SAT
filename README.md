# Anson PhaseLock-SAT (Mobile Build)

A mobile-safe experimental SAT solver framework focused on adaptive search, multi-agent coordination, and constraint navigation under high-density regimes.

This repository contains a research prototype designed to explore solver behavior on constrained devices (e.g., phones, low-RAM systems). The implementation emphasizes stability, low memory overhead, and fast iteration without multiprocessing or native extensions.

> ⚠️ Core algorithmic mechanisms and tuning strategies are intentionally abstracted at a high level in this public repository.

---

## ✨ Features

- Mobile-safe single-file Python build  
- Multi-agent (multi-"planet") coordination model  
- Adaptive perturbation and stabilization phases  
- Constraint pressure tracking & hot-variable detection  
- Optional CSV logging for experimental analysis  
- Designed for low-RAM, low-CPU environments  

---

## 🛠 Requirements

- Python 3.9+  
- No external dependencies  
- Runs in mobile Python environments (iOS Python runners, Termux, etc.)

---

## 🚀 Usage

```bash
python3 main.py --door PHASE --planets 4 --secs 6 --ladder 3.30,4.50,4.80,4.90 --trials 3
```

---

### ✅ Next 2 steps (quick):

1. On GitHub, click **"Add README.md"**
2. Paste this text → **Commit**
