FROM dlanguage/dmd:2.074.0

RUN apt-get update \
 && apt-get install -y curl git \
 && curl -fsSL https://github.com/antirez/linenoise/archive/1.0.tar.gz | tar -zxf - \
 && cd linenoise-1.0 && cc -shared -fPIC linenoise.c -o /lib/liblinenoise.so \
 && git clone https://github.com/drepl/drepl.git \
 && cd drepl && dub build && mv drepl /bin/drepl && cd .. && rm -rf drepl \
 && apt-get auto-remove -y curl git

ENTRYPOINT ["drepl"]
