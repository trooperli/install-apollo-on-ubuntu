# Install Baidu Apollo on Ubuntu 14.04
**Prerequisite**: Ubuntu 14.04 with Nvidia GPU

## Install nvidia driver and cuda
There are two ways of installing cuda and nvidia gpu, one is deb, the other is runfile. Please do use the deb one, considering there is a bug that you won't be able to login to the system if you use the runfile installation. Please follow the [link](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) for detailed instructions.

## Fork the Apollo repository
1. Install git lfs
<pre><code>curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
</code></pre>
