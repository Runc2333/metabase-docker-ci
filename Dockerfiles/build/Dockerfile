FROM ubuntu:20.04

ENV FC_LANG en-US LC_CTYPE en_US.UTF-8

# coreutils:    needed for the basic tools
# ttf-dejavu:   needed for POI
# fontconfig:   needed for POI
# bash:         various shell scripts
# yarn:         frontend building
# nodejs:       frontend building
# git:          ./bin/version
# curl:         needed by script that installs Clojure CLI & Lein

# Install curl, git, bash, coreutils, ttf-dejavu, fontconfig, JDK 11
RUN apt-get update ; \
    DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install -y curl git bash coreutils ttf-dejavu fontconfig rlwrap openjdk-11-jdk; \
    apt-get clean

# Setup Leiningen environment
RUN curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -o /usr/local/bin/lein ; \
    chmod +x /usr/local/bin/lein ; \
    /usr/local/bin/lein upgrade

# Setup Clojure CLI environment
RUN curl -O https://download.clojure.org/install/linux-install-1.11.1.1200.sh ; \
    chmod +x linux-install-1.11.1.1200.sh ; \
    ./linux-install-1.11.1.1200.sh

# Setup nvm environment and install nodejs 14 & yarn
ENV NODE_VERSION=14.21.1
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
ENV NVM_DIR=/root/.nvm
RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
RUN npm install -g yarn

CMD ["/bin/sh"] 