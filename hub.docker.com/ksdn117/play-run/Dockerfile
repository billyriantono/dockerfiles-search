FROM ksdn117/play-framework
MAINTAINER	ksdn117 <ksdn117@gmail.com>

# ENV USERNAME ksdn117
# ENV REPO https://github.com/${USERNAME}
# ENV APPNAME example-app
# ENV DIR play_projects

RUN apt-get install -y git
RUN mkdir play_projects
RUN git clone https://github.com/ksdn117/example-app.git /play_projects/example-app

WORKDIR /play_projects/example-app
CMD ["activator ~run"]
EXPOSE 9000 80
