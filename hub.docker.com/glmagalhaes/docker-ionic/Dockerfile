FROM beevelop/ionic

LABEL maintainer="glmahalhaes@hotmail.com"

RUN apt-get update && apt-get install -y build-essential python-dev python-pip && apt-get clean
RUN mkdir -p "${ANDROID_HOME}/licenses" 
RUN echo -e "\n8933bad161af4178b1185d1a37fbf41ea5269c55" > "${ANDROID_HOME}/licenses/android-sdk-license" 
RUN echo -e "\n84831b9409646a918e30573bab4c9c91346d8abd" > "${ANDROID_HOME}/licenses/android-sdk-preview-license" 
RUN echo -e "\nd975f751698a77b662f1254ddbeed3901e976f5a" > "${ANDROID_HOME}/licenses/intel-android-extra-license"
