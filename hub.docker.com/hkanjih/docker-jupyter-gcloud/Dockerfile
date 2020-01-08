FROM jupyter/minimal-notebook:latest

COPY *.ipynb /home/jovyan/work/

USER root

RUN apt-get update && apt-get install -y curl


# Downloading gcloud package
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz

# Installing the package
RUN mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh

RUN fix-permissions /usr/local/gcloud/
RUN fix-permissions /home/jovyan/.config/gcloud/
RUN fix-permissions /home/jovyan/work/



USER $NB_UID
# Adding the package path to local
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin
# Install app dependencies
RUN pip install google-cloud --user
RUN pip install google-api-python-client --user
RUN pip install oauth2client --user