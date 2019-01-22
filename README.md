# Install Baidu Apollo on Ubuntu 14.04
**Prerequisite**: Ubuntu 14.04 with Nvidia GPU

## Install nvidia driver and cuda
There are two ways of installing cuda and nvidia gpu, one is deb, the other is runfile. Please do use the deb one, considering there is a bug that you won't be able to login to the system if you use the runfile installation. Please follow the [link](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) for detailed instructions.

If cuda is successfully installed, in the command line type <pre><code>nvidia-smi</code></pre> you should have similiar content as shown below:
<pre><code>+-----------------------------------------------------------------------------+
| NVIDIA-SMI 410.79       Driver Version: 410.79       CUDA Version: 10.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  Quadro P5000        Off  | 00000000:65:00.0  On |                  Off |
| 27%   42C    P8    10W / 180W |   2406MiB / 16244MiB |      1%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1262      G   /usr/lib/xorg/Xorg                           544MiB |
|    0      2868      G   compiz                                       164MiB |
|    0      3049      G   ...quest-channel-token=4201908428023029925  1694MiB |
+-----------------------------------------------------------------------------+
</code></pre>

## Fork the Apollo repository
1. Install git lfs
<pre><code>curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
sudo apt-get install git-lfs
</code></pre>

2. Fork the apollo
<pre><code>git lfs clone https://github.com/ApolloAuto/apollo.git
git lfs install
git lfs fetch --all
</code></pre>

After step 2, make sure that the content in modules/dreamview/frontend/dist/app.bundle.js is not meta data but actual code. If the content is still meta data, remove the repository with<pre><code>rm -rf apollo</code></pre>and repeat step 2.

3. Install Docker
Please follow the steps given in this [link](https://docs.docker.com/install/linux/docker-ce/ubuntu/) to install docker. This step is pretty straight forward.  

