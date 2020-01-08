# FROM continuumio/miniconda3

# ADD spec-test.txt /tmp/spec-test.txt
# RUN conda create -n PP --file /tmp/spec-test.txt 

# RUN echo "source activate PP" > ~/.bashrc

# ENV PATH /opt/conda/envs/PP/bin:$PATH

FROM ermaker/keras:gpu

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
      graphviz \
    && rm -rf /var/lib/apt/lists/* \
    && conda install -y \
      cudatoolkit=9.0 \
      cudnn=7.3 \
      cupti=9.0.176 \
      pydot \
      jupyter \
      matplotlib \
      seaborn \
      keras-gpu=2.2.4 \
    && conda clean --yes --tarballs --packages --source-cache

VOLUME /notebook
WORKDIR /notebook
EXPOSE 8888
CMD jupyter notebook --no-browser --ip=0.0.0.0 --allow-root --NotebookApp.token= --NotebookApp.allow_origin='*'
