cmake_minimum_required(VERSION 2.6.0 FATAL_ERROR)
project(boundary CXX C)

if(NOT CUDA_SDK_ROOT_DIR)
  set(CUDA_SDK_ROOT_DIR /usr/local/cuda/samples)
endif()
if(NOT CUDA_TOOLKIT_ROOT_DIR)
  set(CUDA_TOOLKIT_ROOT_DIR /usr/local/cuda)
endif()

find_package(CUDA REQUIRED)

set(CUDA_NVCC_FLAGS
  --ptxas-options=-v -O3 -ftz=true
  -prec-div=false -prec-sqrt=false -use_fast_math
)

#set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS} -arch=sm_35) # Kepler
set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS} -arch=sm_61) # Pascal

include_directories(lib)

add_subdirectory(lib)
add_subdirectory(src)
