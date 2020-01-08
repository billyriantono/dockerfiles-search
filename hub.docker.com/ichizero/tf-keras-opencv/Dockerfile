FROM ichizero/cuda-opencv:latest

LABEL maintainer="ichizero"

RUN apt update && \
  apt install -y x11-apps \
  python3-tk && \
  apt clean

RUN pip3 install  --no-cache-dir \
  Pillow \
  hdf5storage \
  h5py \
  ipykernel \
  jupyter \
  matplotlib \
  numpy \
  pandas \
  scipy \
  sklearn \
  cython \
  argparse \
  py3nvml \
  tqdm \
  requests \
  fire \
  dill

RUN pip3 install  --no-cache-dir \
  tensorflow-gpu \
  keras

# For CUDA profiling, TensorFlow requires CUPTI.
ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH

RUN ln -s -f /usr/bin/python3 /usr/bin/python
