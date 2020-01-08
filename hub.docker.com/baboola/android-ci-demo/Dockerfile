FROM baboola/android-sdk-tools-linux-4333796

# Get SDK Platform packages and SDK Tools
# To get a full list of available options you can use:
#  sdkmanager --list --verbose

RUN sdkmanager 'platforms;android-22'
RUN sdkmanager 'platforms;android-19'
RUN sdkmanager 'extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2'
RUN sdkmanager 'extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2'
RUN sdkmanager 'extras;google;m2repository'
RUN sdkmanager 'extras;android;m2repository'
RUN sdkmanager 'extras;google;google_play_services'

# SDKs
# Please keep these in descending order!
# The `yes` is for accepting all non-standard tool licenses.

# Please keep all sections in descending order!
RUN yes | sdkmanager \
    "platforms;android-22" \
    "platforms;android-19" \
    "extras;android;m2repository" \
    "extras;google;m2repository" \
    "extras;google;google_play_services" \
    'extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2' \
    "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2" \
    'extras;google;google_play_services' \
    
