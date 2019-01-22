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
**1. Install git lfs**
<pre><code>curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
sudo apt-get install git-lfs
</code></pre>

**2. Fork the apollo**
<pre><code>git lfs clone https://github.com/ApolloAuto/apollo.git
git lfs install
git lfs fetch --all
</code></pre>

After step 2, make sure that the content in modules/dreamview/frontend/dist/app.bundle.js is not meta data but actual code. If the content is still meta data, remove the repository with<pre><code>rm -rf apollo</code></pre>and repeat step 2.

**3. Install Docker**

Please follow the steps given in this [link](https://docs.docker.com/install/linux/docker-ce/ubuntu/) to install docker. This step is pretty straight forward.  

**4. Build and Release the Docker Container**

Please follow the steps given in the [link](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_build_and_release.md) to build and release the container.

Make sure to build cuda in the docker:
<pre><code># If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU containers
docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
sudo apt-get purge -y nvidia-docker

# Add the package repositories
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update

# Install nvidia-docker2 and reload the Docker daemon configuration
sudo apt-get install -y nvidia-docker2
sudo pkill -SIGHUP dockerd

# Test nvidia-smi with the latest official CUDA image
docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
</code></pre>

**5. Run Apollo**

Please follow the steps given in the [link](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_launch_Apollo.md) to run apollo. Use the following commands to get into the dev container:
<pre><code>bash docker/scripts/dev_start.sh
bash docker/scripts/dev_into.sh
</code></pre>

Use the foolwoing command to start and stop Apollo:
<pre><code>bash scripts/bootstrap.sh start
bash scripts/bootstrap.sh stop
</code></pre>


