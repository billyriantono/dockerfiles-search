FROM designmynight/ubuntu16.04-build-tools:latest

RUN gem install fpm-cookery

COPY . /data

CMD fpm-cook package -t ${TARGET} -p ${PLATFORM} --pkg-dir=${PKG_DIR} ${RECIPE_FILE}