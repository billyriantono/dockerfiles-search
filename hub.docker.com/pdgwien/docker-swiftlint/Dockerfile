FROM swift:4.0.3
LABEL maintainer "Patrick Grosslicht <patrick@grosslicht.com>"

ENV SWIFTLINT_REVISION="master"

RUN git clone --branch $SWIFTLINT_REVISION https://github.com/realm/SwiftLint.git && \
    cd SwiftLint && \
    swift build --configuration release --static-swift-stdlib && \
    mv `swift build --configuration release --static-swift-stdlib --show-bin-path`/swiftlint /usr/bin && \
    cd .. && \
    rm -rf SwiftLint

# Print Installed SwiftLint Version
RUN swiftlint version
CMD ["swiftlint", "lint"]
