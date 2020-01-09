FROM alpine:3.8 
LABEL maintainer "Alexander Pehm <alexander@alexanderpehm.at>"

RUN apk add --no-cache bash make curl tar gzip tzdata git vim openssh-client

ENV HOME /home/user
RUN addgroup -g 1000 -S user && \
    adduser -u 1000 -S user -G user -h $HOME

RUN curl -L https://github.com/todotxt/todo.txt-cli/archive/v2.11.0.tar.gz | tar xvz && \
    cd todo.txt-cli-2.11.0 && make && make install CONFIG_DIR=$HOME
COPY todotxt/config $HOME/.todo/
RUN mkdir /home/user/.todo.actions.d && cd /home/user/.todo.actions.d && \
    curl -L https://raw.githubusercontent.com/alepeh/todo.txt-cli/note/todo.actions.d/note > note && \
    curl -L https://raw.githubusercontent.com/alepeh/todo.txt-cli/note/todo.actions.d/archive > archive && \
    curl -L https://raw.githubusercontent.com/alepeh/todo.txt-cli/note/todo.actions.d/del > del && \
    curl -L https://raw.githubusercontent.com/alepeh/todo.txt-cli/note/todo.actions.d/rm > rm
RUN chmod +x -R /home/user/.todo.actions.d

COPY bash/profile $HOME/.profile

RUN mkdir $HOME/workspace
RUN chown -R user:user $HOME 
WORKDIR $HOME
USER user
