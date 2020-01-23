FROM homeassistant/home-assistant:0.79.3

# remove existing python
RUN pip3 uninstall -y python_openzwave

RUN pip3 install --upgrade cython==0.24.1

# install new (dev) version of python_openzwave
RUN pip3 install --no-cache-dir 'python_openzwave==0.4.4' --install-option="--flavor=ozwdev"

# Use if we're using a different ozw version than hass
# replace component requirement 0.4.9 with 0.4.4
RUN sed -i 's/0.4.9/0.4.4/' /usr/src/app/homeassistant/components/zwave/__init__.py
