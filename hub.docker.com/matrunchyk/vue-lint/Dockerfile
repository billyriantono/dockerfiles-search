FROM node
LABEL maintainer=serhii@digitalidea.studio

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# RUN sysctl -w net.ipv6.conf.all.disable_ipv6=1
# RUN sysctl -w net.ipv6.conf.default.disable_ipv6=1
# RUN curl -sL https://deb.nodesource.com/setup_8.x | bash
# RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
# RUN echo "deb http://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list
# RUN apt-get update
# RUN apt-get install -y nodejs yarn
CMD ['/usr/local/bin/npm', 'install']

ENTRYPOINT ['./node_modules/.bin/eslint', '--ext .js,.vue', 'resources/assets/js --fix']

# , './node_modules/.bin/babel-node --presets es2015 node_modules/cross-env/dist/bin/cross-env.js BABEL_ENV=test karma start resources/assets/js/tests/build/karma.conf.js']

