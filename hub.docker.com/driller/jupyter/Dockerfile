FROM driller/jupyter:base

# install nodejs
RUN apt-get update \
    && apt-get install -y curl \
    && curl -sL https://deb.nodesource.com/setup_12.x | bash - \
    && apt-get install -y nodejs

# Install Python packages
RUN pip install jupyterlab
RUN chmod -R g+w,o+w /usr/local/share/jupyter/lab/
