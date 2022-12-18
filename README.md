## README for Schroedinger Equation Solvers
#### Stan Mohler, Dec. 2022

The Python apps here solve the Schroedinger equation of Quantum Mechanics.  

The code uses PyTorch to access your machine's GPUs.  I run on my Windows
Anaconda prompt, since my WSL can't access the GPUs.  

The instructions below assume you want to run on a GPU, but you don't need to.

### Set up your environment

1. Install Miniconda.  You can get it at [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html).  
2. Browse to [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/).  
3. Select your OS, "Conda" and "Python".
4. See the CUDA "compute platform" versions compatible with PyTorch.  
5. Also note the recommended `conda install` command.  You will use it soon.  
6. In a terminal, try the command below.
```
        nvcc --version
```
7. Did the command work AND provide a CUDA version identified in the PyTorch site above?  (E.g., "CUDA compilation tools, release 11.7")  If so, proceed to step 9.
8. Otherwise, you need to install a version of the CUDA Toolkit identified in the PyTorch site above.  
   1. Browse to [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads).  
   2. Find a CUDA version identified by the PyTorch site above, maybe the highest compatible one.  You might need to scroll down and click on **Archive of Previous CUDA Releases**.   
   3. Download it.
   4. Install it.
9. Run the `conda create` command based on the `conda install` command identified for you in Step 5 above, **but with the following additions:**
```
        -c conda-forge pandas matplotlib pycuda notebook holoviews
```
        For me, the complete command was:
```
        conda create -n qmtorch -c pytorch -c nvidia -c conda-forge pytorch torchvision torchaudio pytorch-cuda=11.7 pandas matplotlib pycuda notebook holoviews
```
10. Then run the commands below to launch Python and verify that you can import PyTorch, and see your GPUs.  
```
        python
        >>> import torch
        >>> import pycuda.driver as cuda
        >>> import pycuda.autoinit
        >>> cuda.init()
        >>> torch.cuda.current_device()
        0
        >>> cuda.Device(0).name()
        'NVIDIA GeForce RTX 2060'
        >>> availableBytes, totalBytes = cuda.mem_get_info()
        >>> availableBytes/1e9    # show available video memory (GB)
        5.391187968
        >>> totalBytes/1e9        # show total video memory (GB)
        6.442123264
```
### Run the code
1. Launch an Anaconda terminal.  
2. Launch the Jupyter Notebook from the terminal:
```
        conda activate qmtorch
        jupyter notebook
```
3. Run all the Notebook cells.
