FROM nginx:latest

MAINTAINER Milo Casagrande <milo.casagrande@linaro.org>
LABEL Version="1.0" Description="Customized nginx container image for git://ci"

COPY nginx.conf /etc/nginx/nginx.conf
COPY nginx-custom.conf /etc/nginx/conf.d/

# Copy the websites.
RUN rm /etc/nginx/conf.d/default.conf
RUN mkdir -p /etc/nginx/sites-enabled/

COPY websites/signup.conf /etc/nginx/sites-enabled/00-signup.conf
COPY websites/artifacts.conf /etc/nginx/sites-enabled/01-artifacts.conf
COPY websites/hawkbit.conf /etc/nginx/sites-enabled/02-hawkbit.conf
COPY websites/lava.conf /etc/nginx/sites-enabled/03-lava.conf
