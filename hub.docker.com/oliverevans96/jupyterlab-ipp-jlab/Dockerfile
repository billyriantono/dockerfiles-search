FROM jupyter/scipy-notebook

USER root
USER jovyan

COPY env.yml /tmp/env.yml
RUN conda env update -f=/tmp/env.yml -n base

RUN conda install -c conda-forge jupyterlab \
                                 ipywidgets \
                                 ipyvolume \
                                 bqplot \
                                 plotly \
                                 ipyleaflet

RUN jupyter labextension install \
    @jupyter-widgets/jupyterlab-manager \
# "Not a valid origin" error. I guess I'm missing a cert or something
#    @jupyterlab/google-drive \
    @jupyterlab/plotly-extension \
    bqplot \
    ipyvolume \
    jupyter-leaflet \
    jupyterlab_vim \
    @jupyterlab/toc


COPY jlab/WidgetTest.ipynb /home/jovyan

CMD ["start.sh", "jupyter", "lab"]
