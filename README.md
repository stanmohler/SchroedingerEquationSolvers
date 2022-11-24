
## README for Schroedinger Equation Solvers

The Python apps here solve the Schroedinger equation of Quantum Mechanics.  

The code uses PyTorch to access your machine's GPUs.  I run on my Windows
Anaconda prompt, since my WSL can't access the GPUs.  

The instructions below assume you want to run on a GPU, but you don't need to.

### Set up your environment
* Identify whether you already have the CUDA toolkit:
```
        nvcc --version
```
* No 'nvcc' command?  Identify available CUDA driver versions for your machine using the site below.
Click on the "Archive of Previous CUDA Releases" too.
    [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)
* Determine a **conda installation command** that uses one of the CUDA versions, using configurator here:
    [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
* If you don't have the CUDA version you identified, download the installer from the NVIDIA link above.  Install it.
* Run the conda installation command that pytorch.org identified for you in the step before last, but **with some extra packages**.  
My machine had CUDA Toolkit 11.6.  In the Windows Anaconda terminal, run the conda command similar to the one that was appropriate
for me, shown below:  
```
        conda create -n torch -c pytorch -c conda-forge pytorch torchvision torchaudio cudatoolkit=11.6 pandas matplotlib pycuda notebook holoviews
```
* Then launch python.  Run the commands below to verify that you can import PyTorch, and see your GPUs.  
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
Launch the Jupyter Notebook like so:
```
        jupyter notebook
```
