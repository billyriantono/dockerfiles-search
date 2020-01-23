from frolvlad/alpine-miniconda3

RUN conda install --quiet --yes \
  numpy \
  notebook \
  ipywidgets \
  scipy \
  scikit-learn \
  scikit-image \
  pandas \
  pandas-profiling && \
  conda clean -tipsy && \
  jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
  mkdir /notebooks

VOLUME /notebooks
ENTRYPOINT jupyter notebook --no-browser --ip=0.0.0.0 --notebook-dir=/notebooks --allow-root
EXPOSE 8888



