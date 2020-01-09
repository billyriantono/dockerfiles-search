FROM studioibizz/production-php71

# Copied custom configuration for alias and MySQl
COPY conf/vhost.conf /etc/httpd/conf.d/wingzz-vhost.conf
COPY conf/.my.cnf /root/.my.cnf

# install php7 development tools
RUN \
	yum -y install \
		php-devel \
		php-xdebug
COPY ini/50-xdebug.ini /etc/php.d/50-xdebug.ini

# Install mysql client to communicate with other (mysql) containers
RUN yum -y install mysql

# Install Pipeline utilities
RUN pear install PHP_CodeSniffer

# Install Node.js for installing validation tools
RUN mkdir -p /usr/lib/node_modules
RUN ln -s /usr/lib/node_modules /node_modules

RUN curl -sL https://rpm.nodesource.com/setup_11.x | bash -
RUN yum -y install nodejs zip bzip2

# Install Node build essentials to deal with gulp-favicons installation issues
RUN yum -y install gcc gcc-c++ make

# Set ENV variables since we won't have the docker-compose.yml within our build images
ENV NODE_PATH=/usr/lib/node_modules
ENV CHOKIDAR_USEPOLLING="true"
ENV CHOKIDAR_INTERVAL=1000

# Install Yarn to work with gulpfile
RUN curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo
RUN yum -y install yarn

# Fix for global installed packages
RUN npm -g config set user root

# Install the previous named _global.ps1
RUN npm install -g pnpm
RUN pnpm install -g pnpm
RUN mkdir -p /.pnpm-store
RUN chmod -R 777 /.pnpm-store

RUN npm i -g phantomjs-prebuilt@2.1.16
RUN npm i -g gulp@4.0.2
RUN npm i -g glob@7.1.4
RUN npm i -g gulp-install@1.1.0
RUN npm i -g gulp-rename@1.4.0
RUN npm i -g gulp-concat@2.6.1
RUN npm i -g gulp-imagemin@6.2.0
RUN npm i -g node-sass@4.12.0
RUN npm i -g sass@1.23.0
RUN npm i -g gulp-sass@4.0.2
RUN npm i -g gulp-svg-sprite@1.5.0
RUN npm i -g gulp-uglify@3.0.2
RUN npm i -g gulp-watch@5.0.1
RUN npm i -g gulp-newer@1.4.0
RUN npm i -g require-dir@1.2.0
RUN npm i -g gulp-yarn@2.0.0
RUN npm i -g imagemin-pngquant@8.0.0
RUN npm i -g gulp-autoprefixer@7.0.1
RUN npm i -g gulp-terser@1.2.0
RUN npm i -g gulp-favicons@2.3.1
RUN npm i -g gulp-eslint@6.0.0
RUN npm i -g through2@3.0.1

RUN npm i -g gulp-babel@8.0.0-beta.2
RUN npm i -g @babel/core@7.6.4

RUN npm i -g gulp-combine-mq@0.4.0
RUN npm i -g yargs@14.2.0

RUN npm i -g gulp-rev@9.0.0
RUN npm i -g rev-del@2.0.0

# For older projects
RUN npm i -g gulp-ruby-sass@3.0.0
RUN npm i -g gulp-jshint@2.1.0
RUN npm i -g gulp-clean-css@4.2.0

RUN npm i -g gulp-bower@0.0.15
RUN npm i -g gulp-notify@3.2.0

# Install rbenv / Ruby for older projects
RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv && \
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc && \
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc

ENV PATH /root/.rbenv/shims:/root/.rbenv/bin:$PATH

# Install ruby-build & ruby for older projects
RUN git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build && \
    ~/.rbenv/bin/rbenv install 2.5.1 && \
    ~/.rbenv/bin/rbenv global 2.5.1

# Install bundler & sass-media_query_combiner for older projects
RUN ~/.rbenv/bin/rbenv exec gem install ffi -v 1.11.2
RUN ~/.rbenv/bin/rbenv exec gem install bundler -v 2.0.2
RUN ~/.rbenv/bin/rbenv exec gem install sass-media_query_combiner -v 0.0.7

# Install JSHint and Eslint for checking javascripts
RUN npm install -g eslint
RUN npm install -g jshint

# Install JsonLint to validate json files
RUN npm install -g jsonlint

# Second time to make sure the symbolic link is set
RUN ln -s /usr/lib/node_modules /node_modules

# Add development scripts for use with older and newer devtool versions
RUN mkdir -p /root/scripts/devtool
COPY scripts/devtool/functions.sh /root/scripts/devtool/functions.sh
COPY scripts/devtool/hotfix.php /root/scripts/devtool/hotfix.php
RUN ["chmod", "+x", "/root/scripts/devtool/functions.sh"]
RUN ["chmod", "+x", "/root/scripts/devtool/hotfix.php"]
# Add functions.sh to .bashrc to make it accessible at every location
RUN echo 'source ~/scripts/devtool/functions.sh' >> ~/.bashrc

# Add auto completion actions to bash
RUN mkdir -p /root/scripts/bash
COPY scripts/bash/functions.sh /root/scripts/bash/functions.sh
COPY scripts/bash/composer.json /root/scripts/bash/composer.json
RUN ["chmod", "+x", "/root/scripts/bash/functions.sh"]
# Add functions.sh to .bashrc to make it accessible at every location
RUN echo 'source ~/scripts/bash/functions.sh' >> ~/.bashrc
CMD ["/root/scripts/bash/functions.sh"]

#Copied scripts for validation
COPY scripts/wingzz.sh /usr/local/bin/wingzz
COPY scripts/wingzz-validate /usr/local/bin/wingzz-validate
RUN ["chmod", "-R", "+x", "/usr/local/bin"]

# Added index to show all local projects
COPY scripts/index.php /var/www/index.php

# Copied script file to run every time
COPY scripts/start.sh /root/scripts/start.sh
RUN ["chmod", "+x", "/root/scripts/start.sh"]

# Set dir projects as working directory
WORKDIR /projects

CMD ["/root/scripts/start.sh"]