FROM mawall/ubuntu16.04_base

# Packages
RUN apt-get update && apt-get install -y libpcl-dev=1.7.2-14build1
RUN pip install -U setuptools && \
    pip install         \
        python-pcl
RUN conda install -y    \
        matplotlib      \
        numpy           \
        pandas          \
        scipy           \
        scikit-learn