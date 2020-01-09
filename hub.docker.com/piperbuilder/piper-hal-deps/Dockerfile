FROM piperbuilder/raspbian-builder

RUN [ "cross-build-start" ]

WORKDIR /home/piper/piper-hal
COPY . ./

# Remove all files leaving only essential ones needed for compiling external dependencies
RUN find . -not \( -name "Cargo.toml" -or -name "Cargo.lock" -or -name "lib.rs" -or -name "main.rs" -or -name "build.rs" \) -type f -exec rm -f {} \;

# Remove local dependencies in master config file
RUN find . -path "./Cargo.toml" -exec bash -c "sed -i -e /piper-hal/d {}" \;
RUN find . -path "./Cargo.toml" -exec bash -c "sed -i -e /rpi-grove-color-sensor/d {}" \;
RUN find . -path "./Cargo.toml" -exec bash -c "sed -i -e /rpi-grove-temperature-sensor/d {}" \;
RUN find . -path "./Cargo.toml" -exec bash -c "sed -i -e /rpi-grove-ultrasonic-rangefinder/d {}" \;
RUN find . -path "./Cargo.toml" -exec bash -c "sed -i -e /rpi-led-matrix/d {}" \;
RUN find . -path "./Cargo.toml" -exec bash -c "sed -i -e /piper-controller/d {}" \;

# Remove local dependencies in all sub-projects' config files
RUN find . -name "Cargo.toml" -exec bash -c "sed -i -e /\\\/piper-hal/d {}" \;
RUN find . -name "Cargo.toml" -exec bash -c "sed -i -e /\\\/rpi-grove-color-sensor/d {}" \;
RUN find . -name "Cargo.toml" -exec bash -c "sed -i -e /\\\/rpi-grove-temperature-sensor/d {}" \;
RUN find . -name "Cargo.toml" -exec bash -c "sed -i -e /\\\/rpi-grove-ultrasonic-rangefinder/d {}" \;
RUN find . -name "Cargo.toml" -exec bash -c "sed -i -e /\\\/rpi-led-matrix/d {}" \;
RUN find . -name "Cargo.toml" -exec bash -c "sed -i -e /\\\/piper-controller/d {}" \;

# Place dummy code in remaining Rust files
RUN find . \( -name "main.rs" -or -name "lib.rs" -or -name "build.rs" \) -exec bash -c "echo 'fn main() { println!('""'\"Dummy\"'""') }' > {}" \;

# Copy full local firmata codebase back in
COPY ./firmata ./firmata

# Compile external dependencies only
RUN /bin/bash -c "source $HOME/.cargo/env && cargo build --release"

RUN [ "cross-build-end" ]

CMD [ "bash" ]
