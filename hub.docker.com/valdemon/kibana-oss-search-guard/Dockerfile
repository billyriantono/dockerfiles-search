ARG COMPAT=6.6.1
FROM docker.elastic.co/kibana/kibana-oss:$COMPAT

ARG VERSION=6.6.1-18.1

# Dirty but simple hack to get a rid of https://github.com/elastic/kibana/issues/29464
RUN rm -rf ./node_modules/caniuse-lite/* \
    && rm -rf ./node_modules/browserslist/* \
    && rm -rf ./node_modules/babel-preset-env/node_modules/caniuse-lite \
    && rm -rf ./node_modules/babel-preset-env/node_modules/browserslist \
    && curl -s $(curl -s https://registry.npmjs.org/browserslist/latest | grep -Po 'tarball":"\K[^"]*') \
    | tar -xvz --strip=1 -C ./node_modules/browserslist \
    && curl -s $(curl -s https://registry.npmjs.org/caniuse-lite/latest | grep -Po 'tarball":"\K[^"]*') \
    | tar -xvz --strip=1 -C ./node_modules/caniuse-lite \
    && cp -R ./node_modules/caniuse-lite ./node_modules/babel-preset-env/node_modules/ \
    && cp -R ./node_modules/browserslist ./node_modules/babel-preset-env/node_modules/

RUN bin/kibana-plugin install --no-optimize https://search.maven.org/classic/remotecontent?filepath=com/floragunn/search-guard-kibana-plugin/$VERSION/search-guard-kibana-plugin-$VERSION.zip

RUN cat ./node_modules/caniuse-lite/package.json | grep version
RUN cat ./node_modules/babel-preset-env/node_modules/caniuse-lite/package.json | grep version

RUN bin/kibana --optimize