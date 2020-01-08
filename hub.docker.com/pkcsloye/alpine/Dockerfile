# --------------------------------------------
# Created by pkcsloye, 2018.01.06
#            My Email is 40018117@qq.com
#
# Project dockerfiles:
#    https://github.com/pkcsloye/dockerfiles
# --------------------------------------------

FROM docker.io/alpine:3.7

RUN  rs="https://mirrors.ustc.edu.cn/alpine/v3.7"   && \
     rf="/etc/apk/repositories"                     && \
     tz="Asia/Shanghai"                             && \
     echo "$rs/main/"        > $rf                  && \
     echo "$rs/community/"  >> $rf                  && \
     apk update                                     && \
     apk upgrade                                    && \
     apk add curl