FROM python:slim

MAINTAINER Seel 459745355@qq.com

# PIP
COPY requirements.txt /root/
COPY jupyter_notebook_config.py /root/
RUN pip install -r /root/requirements.txt
RUN mkdir /root/.jupyter/ && \
    mv /root/jupyter_notebook_config.py /root/.jupyter/  && \
    jupyter contrib nbextension install --user && \
    jupyter nbextensions_configurator enable --user && \
    jupyter nbextension enable splitcell/splitcell && \
    jupyter nbextension enable codefolding/main && \
    jupyter nbextension enable execute_time/ExecuteTime && \
    jupyter nbextension enable varInspector/main && \
    jupyter nbextension enable snippets_menu/main && \
    jupyter nbextension enable code_prettify/autopep8 && \
    jupyter nbextension enable toggle_all_line_numbers/main

RUN mkdir /notebooks
WORKDIR "/notebooks"

EXPOSE 8888
VOLUME ["/notebooks"]
CMD ["/bin/bash", "-c", "jupyter notebook --allow-root"]
