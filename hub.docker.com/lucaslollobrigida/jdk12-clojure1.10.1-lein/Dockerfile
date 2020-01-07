# FROM circleci/clojure:openjdk-11-lein-2.8.3
FROM adoptopenjdk/openjdk12:alpine

WORKDIR /app

RUN apk update
RUN apk add gcc make git bash curl openssh

# Clojure
RUN curl -O https://download.clojure.org/install/linux-install-1.10.1.489.sh
RUN chmod +x linux-install-1.10.1.489.sh
RUN ./linux-install-1.10.1.489.sh
RUN rm linux-install-1.10.1.489.sh
RUN clojure --version &2> /dev/null

# Lein
RUN curl -O https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
RUN chmod u+x lein
RUN mv lein /bin
RUN lein --version 
# &2> /dev/null
