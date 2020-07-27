# tensorflow.cmake



sudo apt install bazel-3.1.0

./configure

bazel build -c opt --copt=-mavx2 --copt=-mfma //tensorflow/tools/pip_package:build_pip_package

./bazel-bin/tensorflow/tools/pip_package/build_pip_package $HOME/pkg/tensorflow_pkg

pip install ../tensorflow_pkg/tensorflow-2.4.0-cp38-cp38-linux_x86_64.whl

bazel build -c opt --copt=-mavx2 --copt=-mfma //tensorflow:libtensorflow_cc.so

bazel build -c opt --copt=-mavx2 --copt=-mfma //tensorflow:install_headers


#CMakeLists.txt for C++ projects
cmake_minimum_required(VERSION 3.3 FATAL_ERROR)
project(example)

#set(TensorflowCC_DIR /usr/local/lib/cmake/tensorflow)

add_executable(example example.cpp)

find_package(TensorflowCC REQUIRED)
target_link_libraries(example TensorflowCC::TensorflowCC)

'# link cuda if it is available
find_package(CUDA)
if(CUDA_FOUND)
  target_link_libraries(example ${CUDA_LIBRARIES})
endif()



