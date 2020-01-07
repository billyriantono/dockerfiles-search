FROM ruverav/nativefier:latest

ENV NAME "Google Stadia"
ENV PLATFORM "windows"
ENV ARCH "x64"
ENV ELECTRON_VERSION "7.1.2"
ENV ICON "stadia.ico"
ENV MIN_WIDTH "1280"
ENV MIN_HEIGHT "800"
ENV STADIA_URL "https://stadia.google.com/home"

WORKDIR /src
COPY --chown=node:node src/ .
RUN chmod +x build.sh

ENTRYPOINT [ "/src/build.sh" ]