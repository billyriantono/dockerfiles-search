FROM continuumio/miniconda3

# Set the ENTRYPOINT to use bash
#ENTRYPOINT [ “/bin/bash”, “-c” ]

#EXPOSE 5000

RUN apt-get update && apt-get install -y \
 libpq-dev \
 build-essential \
&& rm -rf /var/lib/apt/lists/*

# Use the environment.yml to create the conda environment.
ADD DeepLearning.yml /tmp/DeepLearning.yml
WORKDIR /tmp
RUN conda env update -n root --file  DeepLearning.yml

#ADD . /code
#WORKDIR /code
# Use bash to source our new environment for setting up
# private dependencies—note that /bin/bash is called in
# exec mode directly
#WORKDIR /code/shared
#RUN conda  activate  DeepLearningCatsNDogs 

#RUN [ “/bin/bash”, “-c”, “source activate TheEnvironment && python setup.py develop” 

#CMD [ “source activate TheEnvironment && exec python application.py” ]]
