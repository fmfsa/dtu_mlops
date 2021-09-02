---
layout: default
title: M10 - Profiling
parent: S3 - Debugging, Profiling and Logging
nav_order: 2
---

# Profilers
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---



## Profilers

Using profilers can help you find bottlenecks in your code. In this exercise we will look at two different
profilers, with the first one being the [cProfile](https://docs.python.org/3/library/profile.html), pythons
build in profiler.

### Exercises

1️ Run the `cProfile` on the `vae_mnist_working.py` script. Hint: you can directly call the profiler on a
   script using the `-m` arg
   `python -m cProfile [-o output_file] [-s sort_order] (-m module | myscript.py) `
   
2. Try looking at the output of the profiling. Can you figure out which function took the longest to run?

3. To get a better feeling of the profiled result we can try to visualize it. Python does not
   provide a native solution, but open-source solutions such as [snakeviz](https://jiffyclub.github.io/snakeviz/)
   exist. Try installing snakeviz and load a profiled run into it (HINT: snakeviz expect the run to have the file
   format `.prof`).

4. Try optimizing the run! (Hint: The data is not stored as torch tensor)

### Exercises (optional)

In addition to using pythons build-in profiler we will also investigate the profiler that is build into PyTorch already.
Note that these exercises requires that you have PyTorch v1.8.1 installed. You can always check which version you
currently have installed by writing (in python):

```python
import torch
print(torch.__version__)
```

Additionally, it PyTorch needs to be build with Kineto. This mean that if you get the following error when
trying to do the exercises:
```
Requested Kineto profiling but Kineto is not available, make sure PyTorch is built with USE_KINETO=1
```
You will sadly not be able to complete them. However, if not, the exercise will also require you to have the 
tensorboard profiler plugin installed:
``` 
pip install torch_tb_profiler
```

For this exercise we have provided the solution in form of the script `vae_mnist_pytorch_profiler.py` where
we have already implemented the PyTorch profiler in the script. However, try to solve the exercise yourself!

1. The documentation on the new profiler is sparse but take a look at this
   [blogpost](https://pytorch.org/blog/introducing-pytorch-profiler-the-new-and-improved-performance-tool/)
   and the [documentation](https://pytorch.org/docs/stable/profiler.html) which should give you an idea of 
   how to use the PyTorch profiler.

2. Secondly try to implement the profile in the `vae_mnist_working.py` script from the debugging exercises 
   (HINT: run the script with `epochs = 1`) and run the script with the profiler on.
   
3. Try loading the saved profiling run in tensorboard by writing
   ```
   tensorboard --logdir=./log  
   ```
   in a terminal. Inspect the results in the `pytorch_profiler` tab. What is the most computational expensive
   part of the code? What does the profiler recommend that you improve? Can you improve something in the code?

3. Apply the profiler to your own MNIST code.