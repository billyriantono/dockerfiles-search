FROM tedbrookings/pyro:latest
LABEL maintainer="Ted Brookings <tbrookin@broadinstitute.org>"

RUN conda config --prepend channels conda-forge \
    && conda update -n base -c defaults conda \
    && conda update --all -y \
    && conda install -y -c bioconda pybedtools pytabix \
    && conda install -y \
        seaborn matplotlib jupyter pytest pytest-cov sortedcontainers psutil \
        memory_profiler line_profiler scipy scikit-learn pandas dask pytables \
        py-xgboost-gpu keras-gpu intervaltree pysam \
        hyperopt autograd \
    && apt update && apt install -y cmake \
    && pip install --no-cache-dir --upgrade MulticoreTSNE phate \
    && conda clean -ya
