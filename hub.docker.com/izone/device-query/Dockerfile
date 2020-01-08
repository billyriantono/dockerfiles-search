FROM nvidia/cuda:10.0-base
MAINTAINER Leonardo Loures <luvres@hotmail.com>

## Reference
# https://devblogs.nvidia.com/nvidia-docker-gpu-server-application-deployment-made-easy/

RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        cuda-samples-$CUDA_PKG_VERSION \
  \
    && cd /usr/local/cuda/samples/1_Utilities/deviceQuery \
    && make -j$(nproc) \
  \
    && rm -rf /var/lib/apt/lists/*

CMD /usr/local/cuda/samples/1_Utilities/deviceQuery/deviceQuery
