#
# Image to run various api tools based on
#  node and python.
#
FROM node:11

# Install python-yaml.
RUN apt-get update && apt-get install python-yaml

ADD Dockerfile /
RUN npm i npm@latest -g
RUN npm install -g git+https://github.com/LucyBot-Inc/api-spec-converter.git --unsafe-perm=true --allow-root

ENTRYPOINT ["/usr/local/bin/api-spec-converter"]
CMD /usr/local/bin/api-spec-converter
