FROM jerry153fish/chrome-base 
RUN apt-get -qq update && apt-get -y -qq install git
ENV aes.docker=true
RUN mkdir /app
RUN chown -R javauser:javauser /app
USER javauser
WORKDIR /app 
