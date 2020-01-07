FROM microsoft/dotnet:2.2-runtime
RUN apt-get -y update
RUN apt-get -y install apt-transport-https wget gnupg
RUN echo "deb https://notesalexp.org/tesseract-ocr/stretch/ stretch main" | tee -a /etc/apt/sources.list
RUN echo "deb https://notesalexp.org/tesseract-ocr/tessdata_best/ stretch main" | tee -a /etc/apt/sources.list
RUN wget -O - https://notesalexp.org/debian/alexp_key.asc | apt-key add -
RUN apt-get -y update -oAcquire::AllowInsecureRepositories=true
RUN apt-get -y install notesalexp-keyring -oAcquire::AllowInsecureRepositories=true
RUN apt-get -y update
RUN apt-get -y install ghostscript imagemagick tesseract-ocr tesseract-ocr-deu
