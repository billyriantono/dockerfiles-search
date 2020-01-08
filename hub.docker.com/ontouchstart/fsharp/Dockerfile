FROM microsoft/dotnet:2.0.5-sdk-2.1.4-stretch 
RUN apt-get update -y
RUN apt-get upgrade -y
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update -y
RUN apt-get install -y emacs-nox build-essential unzip git fsharp nodejs yarn
RUN mono --version
RUN dotnet --version
RUN node -v
RUN yarn -v
RUN git clone git://github.com/fsharp/emacs-fsharp-mode.git
RUN cd emacs-fsharp-mode/ && make install
COPY ./init.el /root/.emacs.d/
