FROM jupyter/scipy-notebook

RUN conda install --quiet --yes \
        Pillow \
        h5py \
        ipykernel \
        jupyter \
        matplotlib \
        numpy \
        pandas \
        scipy \
        tensorflow \
        xlrd \
        keras \
        altair \
        bokeh
        
RUN pip install --user --upgrade git+https://github.com/jpmml/sklearn2pmml.git
#        tensorflow-serving-api # https://github.com/tensorflow/tensorflow/issues/13805
