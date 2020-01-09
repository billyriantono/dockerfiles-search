FROM indee/wordpress-build-tools

WORKDIR /app/wp-content/themes/jonjoe

ADD package.json \
    ./
RUN npm install

ADD . .

RUN gulp build \
    && rm -rf ./node_modules

WORKDIR /app/wp-content/plugins

RUN rm -rf akismet \
    && rm hello.php


# Plugins
ADD https://downloads.wordpress.org/plugin/custom-post-type-ui.zip \
    https://downloads.wordpress.org/plugin/advanced-custom-fields.zip \
    https://downloads.wordpress.org/plugin/cloudflare-flexible-ssl.zip \
    https://downloads.wordpress.org/plugin/two-factor-auth.zip \
    ./

RUN unzip -o "./*.zip" \
    && rm *.zip
