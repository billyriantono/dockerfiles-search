FROM jupyter/scipy-notebook

ENV JUPYTER_ENABLE_LAB=true

RUN pip install \
        aria2p \
        cairosvg \
        geoip2 \
        ipyleaflet \
        ipympl \
        ipython-sql \
        plotly \
        pygal \
        quantities \
        simplejson

RUN jupyter labextension install \
        @jupyter-widgets/jupyterlab-manager \
        @jupyterlab/geojson-extension \
        @jupyterlab/plotly-extension \
        jupyter-leaflet \
        jupyter-matplotlib

RUN conda install -c conda-forge -c QuantStack -c pytorch \
        pytorch-cpu \
        torchvision-cpu \
        xeus-cling \
        xwidgets
