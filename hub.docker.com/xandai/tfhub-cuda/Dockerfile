ARG JUPYTERHUB_CUDA_VERSION=0.1.0

FROM xandai/jupyterhub-cuda:${JUPYTERHUB_CUDA_VERSION}

ARG NUMPY_VERSION='1.16.2'
ARG PANDAS_VERSION='0.24.2'
ARG SCIKIT_LEARN_VERSION='0.20.3'
ARG IMAGEIO_VERSION='2.5.0'
ARG MATPLOTLIB_VERSION='3.0.3'
ARG SEABORN_VERSION='0.9.0'
ARG TENSORFLOW_GPU_VERSION='1.13.1'

ARG PIP_PACKAGES="\
numpy==${NUMPY_VERSION} \
pandas==${PANDAS_VERSION} \
scikit-learn==${SCIKIT_LEARN_VERSION} \
imageio==${IMAGEIO_VERSION} \
matplotlib==${MATPLOTLIB_VERSION} \
seaborn==${SEABORN_VERSION} \
tensorflow-gpu==${TENSORFLOW_GPU_VERSION} \
"

RUN python3 -m pip install --no-cache-dir ${PIP_PACKAGES}
