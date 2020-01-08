FROM xomiachuna/miniconda-cuda

# required for tensorflow
RUN conda install -y python=3.6

# core utils
RUN conda install -y -q \
    pandas \
    jupyter \
    scikit-learn \
    matplotlib \
    opencv \
    h5py \
    nltk \
    tensorflow-gpu \
    keras \
    python-graphviz \
    graphviz \
    gensim \
    tqdm \
    xlrd \
    && conda clean --all -y -q
# load all the data for nltk
RUN python -c "import nltk; nltk.download('all')"   
VOLUME /work
WORKDIR /work

RUN echo "jupyter notebook --no-browser --ip=0.0.0.0 --port=8888 --allow-root" > ../run_jupyter.sh

CMD sh ../run_jupyter.sh
