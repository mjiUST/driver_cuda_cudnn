# driver_cuda_cudnn
instruction for the installation of the Nvidia driver + cuda + cudnn
## nvidia driver 375, cuda 8.0, cudnn v5.1 [[1]](https://medium.com/@vivek.yadav/deep-learning-setup-for-ubuntu-16-04-tensorflow-1-2-keras-opencv3-python3-cuda8-and-cudnn5-1-324438dd46f0)
  - nvidia-375 driver:
      * `sudo add-apt-repository ppa:graphics-drivers/ppa`
      * `sudo apt-get update`
      * `sudo apt-get install nvidia-375`
  - cuda download web: https://developer.nvidia.com/cuda-toolkit-archive 
      * .deb:
          - `sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb  # or *-deb file`
          - `sudo apt-key add /var/cuda-repo-<version/Table>/7fa2af80.pub`
          - `sudo apt-get update`
          - `sudo apt-get install cuda`
      * or other format, such as .run
  - cudnn download web: https://developer.nvidia.com/cudnn    You need an account before download.
      * `tar xvf cudnn*.tgz`
      * `cd cuda`
      * `sudo cp */*.h /usr/local/cuda/include/`
      * `sudo cp */libcudnn* /usr/local/cuda/lib64/`
      * `sudo chmod a+r /usr/local/cuda/lib64/libcudnn*`

## cuDNN without sudo (in your home folder) [[2]](http://deeplearning.net/software/theano/library/sandbox/cuda/dnn.html)
  - set the environment variables LD_LIBRARY_PATH, LIBRARY_PATH and CPATH to the directory extracted from the download. 
  - If needed, separate multiple directories with : as in the PATH environment variable.
      * `export CUDNN_ROOT=/home/YourUserName/libs/cudnn`
      * `export LD_LIBRARY_PATH=$CUDNN_ROOT/lib64:$LD_LIBRARY_PATH`
      * `export CPATH=$CUDNN_ROOT/include:$CPATH`
      * `export LIBRARY_PATH=$CUDNN_ROOT/lib64:$LD_LIBRARY_PATH`

## uninstall:
  - cudnn
      * if the cudnn was copied to CUDA_ROOT:
          - `rm /usr/local/cuda/include/cudnn.h`
          - `rm /usr/local/cuda/lib64/libcudnn*`
  - cuda
      * `/usr/local/cuda/bin/uninstallxxx`
      * or `sudo apt remove --purge cuda`    if cuda was install using .deb file.
  - nvidia driver:
      * `sudo apt remove --purge nvidia*`

## errors:
  - raise RuntimeError('Could not find cudnn library (looked for v5[.1])')
      * solution: export LIBRARY_PATH=/usr/local/cuda/lib64:$LIBRARY_PATH
