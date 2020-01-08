FROM studioibizz/production-php71

# Install Pipeline utilities
RUN pear install PHP_CodeSniffer

#Copied scripts for validation
COPY scripts/wingzz.sh /usr/local/bin/wingzz
COPY scripts/wingzz-validate /usr/local/bin/wingzz-validate
RUN ["chmod", "-R", "+x", "/usr/local/bin"]

# Install Node.js for installing validation tools
RUN mkdir -p /usr/lib/node_modules
RUN ln -s /usr/lib/node_modules /node_modules

RUN curl -sL https://rpm.nodesource.com/setup_11.x | bash -
RUN yum -y install nodejs zip bzip2

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
RUN npm i -g phantomjs-prebuilt@2.1.16
RUN npm i -g gulp@4.0.2
RUN npm i -g glob@7.1.4
RUN npm i -g gulp-install@1.1.0
RUN npm i -g gulp-rename@1.4.0
RUN npm i -g gulp-concat@2.6.1
# RUN npm i -g gulp-imagemin@6.2.0
RUN npm i -g node-sass@4.12.0
RUN npm i -g sass@1.23.0
RUN npm i -g gulp-sass@4.0.2
# RUN npm i -g gulp-svg-sprite@1.5.0
RUN npm i -g gulp-uglify@3.0.2
# RUN npm i -g gulp-watch@5.0.1
# RUN npm i -g gulp-newer@1.4.0
RUN npm i -g require-dir@1.2.0
RUN npm i -g gulp-yarn@2.0.0
# RUN npm i -g imagemin-pngquant@8.0.0
RUN npm i -g gulp-autoprefixer@7.0.1
RUN npm i -g gulp-terser@1.2.0
# RUN npm i -g gulp-favicons@2.3.1
RUN npm i -g gulp-eslint@6.0.0
RUN npm i -g through2@3.0.1

RUN npm i -g gulp-babel@8.0.0-beta.2
RUN npm i -g @babel/core@7.6.4

RUN npm i -g gulp-combine-mq@0.4.0
RUN npm i -g yargs@14.2.0

RUN npm i -g gulp-rev@9.0.0
RUN npm i -g rev-del@2.0.0

# Install JSHint and Eslint for checking javascripts
RUN npm install -g eslint
RUN npm install -g jshint

#Install JsonLint to validate json files
RUN npm install -g jsonlint

# Copied scripts for deployment
COPY scripts/deploy /root/deploy

CMD ["/root/scripts/start.sh"]