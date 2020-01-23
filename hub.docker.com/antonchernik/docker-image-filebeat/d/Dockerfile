ARG TF_VERSION=1.14.0
FROM tensorflow/tensorflow:${TF_VERSION}-gpu-py3

COPY data_loader.py  .
RUN ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/local/cuda/lib64/stubs/libcuda.so.1 &&\
    LD_LIBRARY_PATH=/usr/local/cuda/lib64/stubs:${LD_LIBRARY_PATH} python data_loader.py &&\
    rm /usr/local/cuda/lib64/stubs/libcuda.so.1

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

