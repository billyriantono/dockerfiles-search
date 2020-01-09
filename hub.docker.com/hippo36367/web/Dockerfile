FROM nginx:1.15.8 as base

FROM base as build

RUN apt-get update \
    && apt-get install -y --no-install-suggests \
    libluajit-5.1-dev libpam0g-dev zlib1g-dev libpcre3-dev \
    libexpat1-dev git curl build-essential \
    && export NGINX_RAW_VERSION=$(echo $NGINX_VERSION | sed 's/-.*//g') \
    && curl -fSL https://nginx.org/download/nginx-$NGINX_RAW_VERSION.tar.gz -o nginx.tar.gz \
    && tar -zxC /usr/src -f nginx.tar.gz

ARG modules=https://github.com/vozlt/nginx-module-vts.git:v0.1.18

RUN export NGINX_RAW_VERSION=$(echo $NGINX_VERSION | sed 's/-.*//g') \
    && cd /usr/src/nginx-$NGINX_RAW_VERSION \
    && configure_args=''; IFS=','; \
    for module in ${modules}; do \
    module_repo=$(echo $module | sed -E 's@^(((https?|git)://)?[^:]+).*@\1@g'); \
    module_tag=$(echo $module | sed -E 's@^(((https?|git)://)?[^:]+):?([^:/]*)@\4@g'); \
    dirname=$(echo "${module_repo}" | sed -E 's@^.*/|\..*$@@g'); \
    git clone "${module_repo}"; \
    cd ${dirname}; \
    if [ -n "${module_tag}" ]; then git checkout "${module_tag}"; fi; \
    cd ..; \
    configure_args="${configure_args} --add-dynamic-module=./${dirname}"; \
    done; unset IFS \
    && eval ./configure --with-compat ${configure_args} \
    && make modules \
    && mkdir /modules \
    && cp $(pwd)/objs/*.so /modules

FROM base

COPY --from=build /modules/* /etc/nginx/modules/

RUN apt-get update && \
    apt-get -y install --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*

COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf

WORKDIR /app
