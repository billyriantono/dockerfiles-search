FROM tensorflow/tensorflow:1.11.0-gpu-py3
MAINTAINER bboy.seiok <bboy.seiok@deepest.ai>

USER root

WORKDIR /root

# Install wget
RUN apt-get update
RUN apt-get install wget unzip git python-mpi4py cmake libopenmpi-dev -y

# Install StarCraftII
RUN wget -q http://blzdistsc2-a.akamaihd.net/Linux/SC2.4.0.2.zip

# Uncompress StarCraftII
RUN unzip -P iagreetotheeula SC2.4.0.2.zip

# Download StarCraftII Maps
RUN wget -q https://github.com/deepmind/pysc2/releases/download/v1.2/mini_games.zip 

RUN wget -q http://blzdistsc2-a.akamaihd.net/MapPacks/Melee.zip
RUN wget -q http://blzdistsc2-a.akamaihd.net/MapPacks/Ladder2017Season3.zip
RUN wget -q http://blzdistsc2-a.akamaihd.net/MapPacks/Ladder2017Season2.zip
RUN wget -q http://blzdistsc2-a.akamaihd.net/MapPacks/Ladder2017Season1.zip

# Uncompress zip files
RUN unzip mini_games.zip -d ~/StarCraftII/Maps/
RUN unzip -P iagreetotheeula Melee.zip -d ~/StarCraftII/Maps/
RUN unzip -P iagreetotheeula Ladder2017Season3.zip -d ~/StarCraftII/Maps/
RUN unzip -P iagreetotheeula Ladder2017Season2.zip -d ~/StarCraftII/Maps/
RUN unzip -P iagreetotheeula Ladder2017Season1.zip -d ~/StarCraftII/Maps/

# Delete zip files
RUN rm SC2.4.0.2.zip
RUN rm mini_games.zip
RUN rm Melee.zip
RUN rm Ladder2017Season3.zip
RUN rm Ladder2017Season2.zip
RUN rm Ladder2017Season1.zip

# Make Directory
RUN mkdir -p /home/nsml/

# Change permissions
RUN chmod -R 755 /home/nsml

# Move StarCraftII to /home/nsml
RUN mv ~/StarCraftII /home/nsml/

# Change default python 2.7 => 3
RUN /bin/bash -c "ln -sfn /usr/bin/python3 /usr/bin/python"

# Install PySC2 v2.0.1-72-ga9f0934
RUN git clone https://github.com/deepmind/pysc2 && cd pysc2 && git reset --hard a9f093493c4c77adb385602790a480e7f238b97d && sed -i '29 a import sys\nFLAGS(sys.argv)' pysc2/run_configs/__init__.py && python setup.py install

# Install TensorFlow-GPU (Current tensorflow:1.11.0-gpu-py3 seems to have problem as of 2018-10-12)
RUN pip3 uninstall tensorflow && pip3 install --ignore-installed tensorflow-gpu==1.11.0

# fix LD_LIBRARY_PATH
#RUN sed -i '$ a export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/lib64/stubs' ~/.bashrc && source ~/.bashrc
RUN sed -i '$ a export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/lib64/stubs' ~/.bashrc
RUN ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/local/cuda/lib64/stubs/libcuda.so.1
ENV LD_LIBRARY_PATH "$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/lib64/stubs"

# debug
RUN echo $LD_LIBRARY_PATH

# Install baselines v0.1.5
RUN git clone https://github.com/openai/baselines && cd baselines && git reset --hard 28aca637d0f13f4415cc5ebb778144154cff3110 && python setup.py install