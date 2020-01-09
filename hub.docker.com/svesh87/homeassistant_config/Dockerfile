FROM plugins/git
ADD config /config
WORKDIR /config
RUN git clone https://github.com/SergejPr/HomeAssistance-NooLite.git /tmp/ha_noolite && \
    cp -rv /tmp/ha_noolite/custom_components .

FROM homeassistant/home-assistant:latest
RUN pip install noolite-f
COPY --from=0 /config /config
ADD storage /storage
VOLUME ["/storage"]
