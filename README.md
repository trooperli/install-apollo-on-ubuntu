# Install Baidu Apollo on Ubuntu 14.04
**Prerequisite**: Ubuntu 14.04 with Nvidia GPU

## Install nvidia driver and cuda
There are two ways of installing cuda and nvidia gpu, one is deb, the other is runfile. Please do use the deb one, considering there is a bug that you won't be able to login to the system if you use the runfile installation. Please follow the [link](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) for detailed instructions.

## Fork the Apollo repository
1. Install git lfs
<pre><code>
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
sudo apt-get install git-lfs
</code></pre>

2. Fork the apollo
<pre><code>
git lfs clone https://github.com/ApolloAuto/apollo.git
git lfs install
git lfs fetch --all
</code></pre>

After step 2, make sure that the content in modules/dreamview/frontend/dist/app.bundle.js is not meta data but actual code. If the content is still meta data, remove the repository with <pre><code>rm -rf apollo</code></pre> and repeat step 2.

3. Install Docker

