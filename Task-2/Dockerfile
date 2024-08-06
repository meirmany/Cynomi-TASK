FROM jenkins/inbound-agent:jdk17

USER root

ENV MAVEN_VERSION 3.9.8
ENV MAVEN_HOME /opt/maven
ARG MAVEN_DOWNLOAD_SHA512=e5a034a255b5f940d2baa0db1b64bed6ccbc1f568da6b79e37acd92817809c273158f52b2e0e2b942020efc203202f1338f2580590c8fd0ee4fca9bc08679577

# Create Maven user and directories
RUN groupadd --system --gid 1001 maven \
    && useradd --system --gid maven --uid 1001 --shell /bin/bash --create-home maven \
    && mkdir /home/maven/.m2 \
    && chown --recursive maven:maven /home/maven \
    && chmod -R g+w /home/maven/.m2 \
    && usermod -aG maven jenkins \
    && ln --symbolic /home/maven/.m2 /root/.m2 \
    && ln --symbolic /home/maven/.m2 /home/jenkins/.m2

VOLUME /home/maven/.m2

# Set working directory
WORKDIR /home/maven

# Install necessary packages and Maven
RUN apt-get update \
    && apt-get install --yes --no-install-recommends \
        unzip \
        wget \
        bzr \
        git \
        git-lfs \
        mercurial \
        openssh-client \
        subversion \
    && rm --recursive --force /var/lib/apt/lists/* \
    && wget --no-verbose --output-document=maven.zip "https://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.zip" \
    && echo "${MAVEN_DOWNLOAD_SHA512} *maven.zip" | sha512sum --check - \
    && unzip maven.zip \
    && rm maven.zip \
    && mv "apache-maven-${MAVEN_VERSION}" "${MAVEN_HOME}/" \
    && ln --symbolic "${MAVEN_HOME}/bin/mvn" /usr/bin/mvn \
    && apt-get clean

# Install Chrome and ChromeDriver
RUN apt-get update \
    #&& wget http://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_108.0.5359.124-1_amd64.deb \
    && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    #&& chmod 777 google-chrome-stable_108.0.5359.124-1_amd64.deb \
    && chmod 777 google-chrome-stable_current_amd64.deb \
    #&& apt-get install -y ./google-chrome-stable_108.0.5359.124-1_amd64.deb \
    && apt install -y ./google-chrome-stable_current_amd64.deb \
    && wget https://chromedriver.storage.googleapis.com/108.0.5359.71/chromedriver_linux64.zip \
    #&& wget https://developer.chrome.com/docs/chromedriver/downloads#chromedriver_1140573590 \
    && unzip chromedriver_linux64.zip \
    && chmod +x chromedriver \
    && mv chromedriver /usr/bin \
    && rm chromedriver_linux64.zip \
    && apt-get clean

# Set working directory to Jenkins home
WORKDIR /home/jenkins

USER jenkins

