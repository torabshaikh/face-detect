**Install CUDA 10.2 and cudNN**


**Add cuda path**
export PATH=${PATH}:/usr/local/cuda-10.2/bin
export CUDA_HOME=${CUDA_HOME}:/usr/local/cuda:/usr/local/cuda-10.2
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/cuda-10.2/lib64
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/extras/CUPTI/lib64

Copy repo
**To build dlib**
git clone https://github.com/davisking/dlib.git
cd dlib
mkdir build
cd build
cmake ..
cmake --build . --config Release
sudo make install
sudo ldconfig

To use openCV DNN GPU we need to build it with CUDA support
**To build OpenCV**
Install dependencies
`sudo apt-get install libjpeg-dev libpng-dev libtiff-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libgtk-3-dev libatlas-base-dev gfortran`

**Get OpenCV and Contrib**
git clone https://github.com/torabshaikh/opencv.git
git clone https://github.com/opencv/opencv_contrib.git

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_PYTHON3_EXAMPLES=ON -D INSTALL_C_EXAMPLES=OFF -D OPENCV_ENABLE_NONFREE=ON -D WITH_CUDA=ON -D WITH_CUDNN=ON -D OPENCV_DNN_CUDA=ON -D ENABLE_FAST_MATH=1 -D CUDA_FAST_MATH=1 -DCUDA_GENERATION="" -DCUDA_ARCH_BIN="5.2" -DCUDA_ARCH_PTX="5.2" -D WITH_CUBLAS=1 -D OPENCV_EXTRA_MODULES_PATH=$HOME/Documents/opencv/opencv_contrib/modules  -D PYTHON_EXECUTABLE=$(which python) -D PYTHON_DEFAULT_EXECUTABLE=$(which python) -D PYTHON3_EXECUTABLE=$(which python) -D PYTHON3_INCLUDE_DIR=$(python -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") -D PYTHON3_INCLUDE_DIR2=$(python -c "from os.path import dirname; from distutils.sysconfig import get_config_h_filename; print(dirname(get_config_h_filename()))")   -D PYTHON3_NUMPY_INCLUDE_DIRS=$(python -c "import numpy; print(numpy.get_include())") -D BUILD_EXAMPLES=ON    -D BUILD_opencv_python2=OFF  -D WITH_FFMPEG=1 .. >> cmake_log.txt


 cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D INSTALL_C_EXAMPLES=OFF \
-D OPENCV_ENABLE_NONFREE=ON \
-D WITH_CUDA=ON \
-D WITH_CUDNN=ON \
-D OPENCV_DNN_CUDA=ON \
-D ENABLE_FAST_MATH=1 \
-D CUDA_FAST_MATH=1 \
-DCUDA_GENERATION="" \
-DCUDA_ARCH_BIN="5.2" \
-DCUDA_ARCH_PTX="5.2" \
-D WITH_CUBLAS=1 \
-D OPENCV_EXTRA_MODULES_PATH=$HOME/Documents/opencv/opencv_contrib/modules/ \
-D HAVE_opencv_python3=ON \
-D PYTHON_EXECUTABLE=$(which python) \
-D BUILD_EXAMPLES=ON \
-D WITH_FFMPEG=1 >> cmake_log.txt
