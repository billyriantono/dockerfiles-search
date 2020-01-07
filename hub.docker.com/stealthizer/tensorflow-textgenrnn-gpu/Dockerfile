FROM nvidia/cuda:10.0-base-ubuntu18.04

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
	python3 \
	python3-pip \
	python3-setuptools \
	libgomp1 \
	libcudnn7=7.4.1.5-1+cuda10.0 \
	cuda-cublas-10-0 \
        cuda-cufft-10-0 \
        cuda-curand-10-0 \
        cuda-cusolver-10-0 \
	cuda-cusparse-10-0 \
	&& rm -rf /var/lib/apt/lists/*

RUN pip3 install wheel && \
	pip3 install https://github.com/stealthizer/tensorflow-textgenrnn-gpu/raw/master/wheel/tensorflow-1.13.1-cp36-cp36m-linux_x86_64.whl textgenrnn==1.5.0 wheel
