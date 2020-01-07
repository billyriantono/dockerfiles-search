FROM php:7.1-fpm-jessie
WORKDIR /app

#gulp
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
 && apt-get update \
 && apt-get install -y \
 zsh \
 wget \
 git \
 nodejs

RUN npm update \
 && npm install -g --save-dev gulp \
 && npm install -g --save-dev node-sass \
 && npm install -g --save-dev gulp-sass \
 && npm install -g --save-dev gulp-clean-css \
 && npm install -g --save-dev gulp-autoprefixer \
 && npm install -g --save-dev gulp-wrap \
 && npm install -g --save-dev gulp-tap \
 && npm install -g --save-dev gulp-file-include \
 && npm install -g --save-dev gulp-concat gulp-rename gulp-uglify \
 && npm install -g --save-dev gulp-util \
 && npm install -g --save-dev gulp-debug

# WORKDIR /app
# RUN npm link gulp \
#  && npm link gulp-sass \
#  && npm link gulp-clean-css \
#  && npm link gulp-autoprefixer \
#  && npm link gulp-wrap \
#  && npm link gulp-tap \
#  && npm link gulp-file-include \
#  && npm link gulp-concat \
#  && npm link gulp-rename \
#  && npm link gulp-uglify \
#  && npm link gulp-util \
#  && npm link gulp-debug

# oh-my-zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true \
	&& chsh -s /bin/zsh \
	&& chsh -s /bin/zsh www-data

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
WORKDIR /app

EXPOSE 9000
CMD ["php-fpm"]
