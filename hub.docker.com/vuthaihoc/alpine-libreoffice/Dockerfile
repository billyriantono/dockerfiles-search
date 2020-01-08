FROM woahbase/alpine-libreoffice:x86_64

# Update fonts
COPY ./fonts/* /usr/share/fonts/
RUN fc-cache -fv && fc-list

# Set the locale
#RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
#    locale-gen
ENV LANG C.UTF-8  
ENV LANGUAGE C:en  
ENV LC_ALL C.UTF-8    

EXPOSE 9999

ENTRYPOINT java


