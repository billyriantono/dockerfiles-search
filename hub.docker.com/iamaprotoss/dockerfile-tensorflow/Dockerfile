from nvidia/cuda:8.0-cudnn5-devel

RUN apt-get update --fix-missing && apt-get install -y wget \
	&& echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh \ 
    && wget https://repo.continuum.io/archive/Anaconda2-4.2.0-Linux-x86_64.sh -O ~/anaconda.sh \
    && /bin/bash ~/anaconda.sh -b -p /opt/conda \
    && rm ~/anaconda.sh

ENV PATH /opt/conda/bin:${PATH}
ENV TF_BINARY_URL https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-0.11.0-cp27-none-linux_x86_64.whl
RUN conda create -y -n tensorflow python=2.7
RUN /bin/bash -c "source activate tensorflow \
	&& pip install --ignore-installed --upgrade $TF_BINARY_URL \
	&& source deactivate tensorflow"

