FROM node:10.6.0-slim

RUN apt-get update && apt-get install -y curl git && npm cache clean -f && \
    curl -o- -L https://yarnpkg.com/install.sh | bash && yarn global add \
    bower \
    grunt-cli \
    gulp-cli \
    grunt \
    webpack \
    ionic \
    cordova \
    typescript \
    create-react-app \
    create-react-native-app \
    rxjs \
    @vue/cli \
    @vue/cli-init \
    @angular/cli \
    ember-cli \
    karma-cli \
    jasmine \
    n
