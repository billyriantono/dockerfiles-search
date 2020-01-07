FROM jupyter/tensorflow-notebook

# Update tensorflow to 1.4
USER root
#RUN conda install --quiet --yes 'tensorflow=1.4*'
RUN pip install --ignore-installed --upgrade https://github.com/sigilioso/tensorflow-build/raw/master/tensorflow-1.4.0-cp36-cp36m-linux_x86_64.whl
USER $NB_USER


