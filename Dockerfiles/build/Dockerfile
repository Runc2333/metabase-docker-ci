FROM eburypartners/ubuntu-jdk11-maven:latest

ENV FC_LANG en-US LC_CTYPE en_US.UTF-8

# coreutils:    needed for the basic tools
# ttf-dejavu:   needed for POI
# fontconfig:   needed for POI
# bash:         various shell scripts
# yarn:         frontend building
# nodejs:       frontend building
# git:          ./bin/version
# curl:         needed by script that installs Clojure CLI & Lein

# Install curl, git, bash, coreutils, ttf-dejavu, fontconfig
RUN apt-get update ; \
    apt-get install -y curl git bash coreutils ttf-dejavu fontconfig ; \
    apt-get clean

RUN curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -o /usr/local/bin/lein ; \
    chmod +x /usr/local/bin/lein ; \
    /usr/local/bin/lein upgrade ; \
    curl https://download.clojure.org/install/linux-install-1.11.1.1149.sh -o /tmp/linux-install-1.11.1.1149.sh; \
    chmod +x /tmp/linux-install-1.11.1.1149.sh;\
    sh /tmp/linux-install-1.11.1.1149.sh

# Setup nodejs 14 environment
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - ; \
    apt-get install -y nodejs

# Setup yarn environment
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - ; \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list ; \
    apt-get update ; \
    apt-get install -y yarn

CMD ["/bin/sh"] 