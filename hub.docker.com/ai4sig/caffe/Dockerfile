FROM bvlc/caffe:gpu
LABEL maintainer "AI4SIG"

# Install grapthviz
RUN apt-get update && apt-get install -y --no-install-recommends \
        graphviz && \
    rm -rf /var/lib/apt/lists/*

# Install Jupyter
RUN pip install --no-cache-dir jupyter

# Jupyter
EXPOSE 8888
