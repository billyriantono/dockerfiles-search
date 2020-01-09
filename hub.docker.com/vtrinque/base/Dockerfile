FROM fedora:21

MAINTAINER Valentin Trinque <val.trinque@gmail.com>

# create a specific group and user to prevent usage of root access later
RUN groupadd app

RUN useradd \
    --comment "user preventing usage of root" \
    --create-home \
    --gid app \
    --key MAIL_DIR=/dev/null \
    app

# add password to `app` user
RUN echo "app:app" | chpasswd

# can be overriden by setting up a new USER clause or -u option
USER app

# switch to newly created user
WORKDIR /home/app

# create a volume on which you link the code folder
VOLUME /home/app/code

# OPTIONAL CONFIGURATION

# custom prompt : [ user ][ path ] $
# if command return non-zero code, then $ is colored in red
RUN echo "PS1='\e[1;37m[ \e[1;32m\u \e[1;37m][ \e[1;34m\w \e[1;37m] \`if [[ \$? = \"0\" ]]; then echo \"\\[\\e[1;37m\\]\"; else echo \"\\[\\e[1;31m\\]\"; fi\`\$\e[0m '" >> /home/app/.bashrc
