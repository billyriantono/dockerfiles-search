FROM piperbuilder/raspbian-nodejs:2.4.6
MAINTAINER Andrew Guterman <andrew@playpiper.com>

# invoke QEMU binaries for shell calls
RUN [ "cross-build-start" ]

# NodeJS installed version
ARG node_ver=v8.9.1

ENV NODEJS_HOME "/usr/local/lib/nodejs/node-$node_ver/bin"
ENV PATH "$NODEJS_HOME:$PATH"

# Cached work directory
WORKDIR /usr/local/games/pipercode

# Copy files
COPY . /usr/local/games/pipercode/

# Build
ENV NPM_CONFIG_PREFIX "~/.npm-global"
RUN npm install
RUN npm rebuild node-sass
RUN npm run build

# web app install
WORKDIR ../release
RUN npm install

# Copy desktop icon
#ENV HOME /home/pi
#RUN mkdir "${HOME}"
#COPY ./pipercode.desktop $HOME/Desktop/pipercode.desktop
#COPY ./pipercodeicon.png ./pipercodeicon.png

# Symlinks
#RUN ln -s . "${HOME}/pipercode"

# Permissions
#RUN chmod -R 775 .
#RUN chown -R pi:pi .

# end shell calls via QEMU binaries
RUN [ "cross-build-end" ]

CMD ["bash"]

