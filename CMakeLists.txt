# Header
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
CMAKE_POLICY(SET CMP0012 NEW)
PROJECT(hw1)

# Set compiler options
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -std=gnu99 -O3")
SET(MKL_LIBRARIES "${MKLROOT}")
SET(MKL_INCLUDE_DIRS "${CPATH}")

# Source files
SET(HW1_NAIVE dgemm-naive.c benchmark.c)
SET(HW1_BLOCKED dgemm-blocked.c benchmark.c)
SET(HW1_BLAS dgemm-blas.c benchmark.c)

# Include files
LINK_DIRECTORIES(${MKL_LIBRARIES})
INCLUDE_DIRECTORIES(${MKL_INCLUDE_DIRS})
ADD_EXECUTABLE(benchmark-naive ${HW1_NAIVE})
TARGET_LINK_LIBRARIES(benchmark-naive rt mkl_intel_lp64 mkl_sequential mkl_core pthread m dl)
ADD_EXECUTABLE(benchmark-blocked ${HW1_BLOCKED})
TARGET_LINK_LIBRARIES(benchmark-blocked rt mkl_intel_lp64 mkl_sequential mkl_core pthread m dl)
ADD_EXECUTABLE(benchmark-blas ${HW1_BLAS})
TARGET_LINK_LIBRARIES(benchmark-blas rt mkl_intel_lp64 mkl_sequential mkl_core pthread m dl)
