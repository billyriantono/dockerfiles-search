FROM google/dart

RUN apt update \
  && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
  && apt install -y nodejs \
  && pub global activate webdev \
  && export PATH="$PATH":"$HOME/.pub-cache/bin"

RUN npm i -g firebase-tools
