FROM gsscogs/csvlint:latest

# Set Envs
ARG local_ref
ENV LOCAL_REF=$local_ref

# Update and install base packages
RUN apk update
RUN apk add --no-cache bash git python3 python3-dev libstdc++ libxslt-dev libxml2-dev

# Force always clone repo, see: https://stackoverflow.com/questions/36996046/how-to-prevent-dockerfile-caching-git-clone
ADD https://api.github.com/repos/GSS-Cogs/csvw-datacube-validation/git/refs/heads/master version.json
RUN cd /workspace && git clone -b master https://github.com/GSS-Cogs/csvw-datacube-validation /csvw-datacube-validation

# Install all the things
RUN apk add --no-cache --virtual .build-deps gcc g++ musl-dev \
 && pip3 install cython \
 && pip3 install numpy \
 && pip3 install -r /csvw-datacube-validation/requirements.txt \
 && apk del .build-deps

VOLUME /workspace
WORKDIR /workspace

COPY ./run.sh /
RUN chmod +x /run.sh
