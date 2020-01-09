FROM ubuntu:16.04
RUN apt update \
	&& apt install -yf \
	nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
