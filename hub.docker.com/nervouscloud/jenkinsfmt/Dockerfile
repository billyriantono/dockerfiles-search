FROM haskell
RUN apt-get install -y git
RUN git clone https://github.com/maartenJacobs/language-jenkins \
    && cd language-jenkins \
    && stack install
ENTRYPOINT ["jenkinsfmt"]