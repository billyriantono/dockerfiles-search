FROM nvidia/cuda:8.0-devel

ENV DEBIAN_FRONTEND noninteractive

# Set up NVIDIA OpenCL environment
RUN apt-get update -q && apt-get install --no-install-recommends -yq \
    clinfo \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Export useful variables
ENV OCL_LIB /usr/local/cuda/lib64
ENV OCL_INC /usr/local/cuda/include
