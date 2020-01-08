FROM node:10

# get yarn
RUN curl -o- -L https://yarnpkg.com/install.sh | bash

#directory to do the build in
WORKDIR /usr/src/build

#copy all the app app build dependancies
#both package.json and package-lock.json

COPY package*.json ./

#install local dependancies
RUN npm install

#install Global dependancies
RUN npm install --global gatsby-cli

RUN npm install --global --unsafe-perm --arch=x64 --platform=linux --target=8.10.0 sharp

#install amplify CLI dependancies
RUN npm install --global @aws-amplify/cli@multienv

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
         rsync \
         libunwind8 \
         zip \
    && rm -rf /var/lib/apt/lists/*

RUN set -ex \
    && wget https://aka.ms/downloadazcopy-v10-linux \
    && tar -xvf downloadazcopy-v10-linux \
    && cp -f ./azcopy_linux_amd64_*/azcopy /usr/bin/ \
	&& chmod a+x /usr/bin/azcopy

CMD ["azcopy", "--version"]