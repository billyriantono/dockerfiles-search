FROM node:latest //nodeJS'nin son sürümünü indir

MAINTAINER yenidoganbusra@gmail.com

RUN mkdir -p /src/nodeapp //linux'de /src/nodeapp klasörünü aç
WORKDIR /src/nodeapp // bu dosyayı çalışma yeri olarak ata

COPY package.json /src/nodeapp //package.json'u açtığımız klasöre kopyala
RUN npm install // package.json içerisinde node paketlerini yükle
COPY . /src/nodeapp // projedeki tüm dosyaları klasöre taşı

EXPOSE 8080// bu portu kullarak uygulamayı yayınla
CMD ["node", "server.js"] //uygulamayı çalıştırmak için bu komutu kullan

