FROM ajnasz/node-base:1.0

MAINTAINER Lajos Koszti <ajnasz@ajnasz.hu>

# Set instructions on build.
# ONBUILD ADD package.json /app/
ONBUILD ADD . /app

# Define working directory.
WORKDIR /app

EXPOSE 3000

CMD ["npm", "start"]
