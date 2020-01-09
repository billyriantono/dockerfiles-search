FROM continuumio/miniconda3:latest

# Install extra packages if required
RUN apt-get update && apt-get install -y \
    && rm -rf /var/lib/apt/lists/*

# Add the user that will run the app (no need to run as root)
RUN groupadd -r freeass && useradd -r -g freeass freeass

WORKDIR /app

# Install myapp requirements
COPY environment.yml /app/environment.yml

RUN conda config --add channels conda-forge \
    && conda update -n base -c defaults conda \
    && conda env create -n freeass -f environment.yml \
    && rm -rf /opt/conda/pkgs/*

# Install app
#
COPY freeass.py /app/
RUN wget https://www.dropbox.com/s/sjwtqr8qmaaukne/w2vscifi.pkl -q --show-progress
RUN chown -R freeass:freeass /app/*

# Activate app environment
ENV PATH /opt/conda/envs/freeass/bin:$PATH

# Start application
#CMD ["echo", "$TOKEN"]
# for development in shell
# to run with: 
# docker run -it --env-file env.list freeassbot:latest
#ENTRYPOINT [ "/bin/bash" ]

ENTRYPOINT [ "python", "freeass.py" ]