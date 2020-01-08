FROM pyrosix/jupyter-notebook

USER root
# This is needed because requests-kerberos fails to install on debian due to missing linux headers
RUN conda install requests-kerberos -y
RUN chown -R $NB_UID:users /home/jovyan/.local/

USER $NB_UID

RUN mkdir /home/jovyan/.sparkmagic
COPY sparkmagic_config.json /home/jovyan/.sparkmagic/config.json

USER root
RUN chown $NB_UID:users /home/jovyan/.sparkmagic/config.json

USER $NB_UID

RUN pip install --user --upgrade pip
RUN pip install --user --upgrade --ignore-installed setuptools

RUN pip install widgetsnbextension
RUN jupyter nbextension enable --py --sys-prefix widgetsnbextension
RUN pip install hdijupyterutils
RUN pip install autovizwidget
RUN pip install sparkmagic

USER root
RUN jupyter serverextension enable --py sparkmagic

USER $NB_UID