# Scratch base
FROM radix10/denv-java:base
MAINTAINER "admin@radix10.cn"

# Install jdk and completer ycm java
RUN sudo apt-get install -y openjdk-8-jdk openjdk-8-doc openjdk-8-source \
&& python3 ~/.vim/bundle/YouCompleteMe/install.py --java-completer

# Add lombok
ADD --chown=scratch:users https://projectlombok.org/downloads/lombok.jar .vim/bundle/lombok/lombok.jar

# Copy config file
COPY --chown=scratch:users .config/vim/java .config/vim/java
RUN echo 'source ~/.config/vim/java' >> .vimrc
