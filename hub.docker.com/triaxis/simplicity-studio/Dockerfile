FROM triaxis/simplicity-studio:4-gecko-2.7.0
RUN /opt/SimplicityStudio_v4/studio \
    -application org.eclipse.equinox.p2.director \
    -r ${SILABS_REPOSITORY} \
    -i com.silabs.stack.ble.v2.13.feature.feature.group/2.13.0.0 \
    && rm -rf /opt/SimplicityStudio_v4/p2/org.eclipse.equinox.p2.core/cache
