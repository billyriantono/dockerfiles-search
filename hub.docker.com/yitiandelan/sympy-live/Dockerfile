FROM malexandre/gae:python

MAINTAINER TIANLAN <yitiandelan@outlook.com>

RUN apk --update --no-cache add git \
    && git clone https://github.com/sympy/sympy-live.git /app \
    && git clone https://github.com/sympy/sympy.git /app/sympy \
    && git clone https://github.com/sympy/sympy-web-static.git /app/static \
    && git clone https://github.com/fredrik-johansson/mpmath.git /app/mpmath \
    && apk del ca-certificates libssh2 libcurl pcre git 

EXPOSE 8080

CMD $APPENGINE/dev_appserver.py --host 0.0.0.0 --skip_sdk_update_check=yes /app
