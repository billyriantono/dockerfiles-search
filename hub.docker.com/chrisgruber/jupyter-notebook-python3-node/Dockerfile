# Set the base image using miniconda 
FROM continuumio/miniconda3:4.6.14

# Set environmental variable(s)
ENV ACCEPT_INTEL_PYTHON_EULA=yes

# Set working directory 
WORKDIR /home/notebooks

# Add requirements file 
ADD requirements.txt /app/

# Installs, clean, and update   
RUN apt-get update \
  && apt-get clean \
  && apt-get update -qqq \
  && apt-get install -y -q g++ gcc make \
  && conda config --add channels intel \
  && conda install -y -q intelpython3_full=2019.4 python=3 \ 
  && pip install --upgrade pip \ 
  && pip install -r /app/requirements.txt \
  && pip install jupyter

RUN apt-get install -yq curl software-properties-common

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

RUN apt-get install -y nodejs

RUN npm install -g ijavascript --unsafe-perm

RUN ijsinstall

# Run shell command for notebook on start 
CMD jupyter notebook --port=8888 --no-browser --ip=0.0.0.0 --allow-root