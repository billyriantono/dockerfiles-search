FROM python:3.6

RUN apt update \
    && apt install -y \
    default-jdk \
    default-jre \
    poppler-utils \
    libsm6 \
    libxrender1 \
    libfontconfig1 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /home/src

ADD README.md .
ADD setup.py .
ADD requirements.txt .
ADD examples.py .
ADD server.py .
ADD pdf2words pdf2words
ADD external external

ENV PDFBOX_PATH /home/src/external

WORKDIR ${PDFBOX_PATH}

RUN javac -cp pdfbox-app-2.0.15.jar PrintTextLocations.java

WORKDIR /home/src

RUN python setup.py install

EXPOSE 8080

ENTRYPOINT [ "python", "server.py", "-p", "8080" ]