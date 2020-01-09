FROM crossworth/php73-fpm-alpine-exts

RUN apk add --no-cache \
        procps \
        shadow \
        g++ \
        icu-dev \
        ncurses-dev \
        make \
        autoconf \
        automake \
        libtool \
        m4

RUN cd /tmp \
    && wget -O source.tar.bz2 https://github.com/FirebirdSQL/firebird/releases/download/R2_5_9/Firebird-2.5.9.27139-0.tar.bz2 \
    && mkdir -p /tmp/firebird \
    && tar --strip=1 -xf source.tar.bz2 -C /tmp/firebird \
    && cd /tmp/firebird \
    # Fix problem with rwlock.h https://github.com/FirebirdSQL/firebird/commit/b91c68bb307e78ce2546feb763686bbba9126505#diff-1e9e657f4b7663621ef0cf16bed99109
    # https://gist.github.com/usmansaleem/1cb81d366fd721bd09b85579dc37aacf
    && sed -i '194s/.*/#if 0/' src/common/classes/rwlock.h  \
    && ./configure --prefix=/opt/firebird --with-system-editline=yes --with-system-icu \
    && make \
    && make silent_install

RUN docker-php-ext-install interbase

CMD ["php-fpm"]