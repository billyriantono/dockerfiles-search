FROM alpine:3.8

# ustc mirrors, it make `apk add` faster in china.
RUN echo "http://mirrors.ustc.edu.cn/alpine/v3.8/main/" > /etc/apk/repositories && \
    echo "http://mirrors.ustc.edu.cn/alpine/v3.8/community/" >> /etc/apk/repositories && \
    apk add --no-cache  \
        perl         && \
    apk add --no-cache --virtual .build-deps \
        ca-certificates    \
        wget               \
        perl-dev           \
        perl-app-cpanminus \
        make               \
        gcc                \
        musl-dev        && \
    cpanm --mirror http://mirrors.163.com/cpan/ \
        Devel::REPL          \
        Term::ReadLine::Perl \
        Term::ReadKey     && \
    apk del .build-deps && \
    rm -rf /root/.cpan /root/.cpanm


ENV DEVEL_REPL_PROFILE Default

CMD ["re.pl"]
