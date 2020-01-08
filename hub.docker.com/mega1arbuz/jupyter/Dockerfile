FROM jupyter/base-notebook

USER root

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y git

USER $NB_UID

RUN conda install --quiet --yes \
    'pandas==0.23.0' \
    'scikit-learn==0.20.3' \
    'tqdm==4.31.1' \
    'plotly==3.2.1' \
    'numpy' \
    'jupyter_contrib_nbextensions' \
    'ipywidgets'

RUN pip install pyconll==1.1.3

RUN jupyter nbextension enable execute_time/ExecuteTime
RUN jupyter nbextension enable collapsible_headings/main
RUN jupyter nbextension enable scratchpad/main
RUN jupyter nbextension enable --py widgetsnbextension

#http://127.0.0.1:8888/?token=12345abcd

ENV JUPYTER_TOKEN='12345abcd'
