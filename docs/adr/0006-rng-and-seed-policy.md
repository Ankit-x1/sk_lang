# RNG and Seed Policy

Use a recorded root seed and explicit NumPy `Generator` streams derived per scenario, and record run inputs and software/data versions so the same run can be reproduced independently of scenario execution order. Reproducibility is conditional on those recorded inputs and does not by itself establish convergence.
