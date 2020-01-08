FROM cibuilds/snapcraft:core18
RUN apt update
COPY . /redisgraph
RUN cd /redisgraph && snapcraft clean && snapcraft
