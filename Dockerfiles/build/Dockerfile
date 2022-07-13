FROM radishgz/centos-jdk11

ENV FC_LANG en-US LC_CTYPE en_US.UTF-8

# coreutils:    needed for the basic tools
# ttf-dejavu:   needed for POI
# fontconfig:   needed for POI
# bash:         various shell scripts
# yarn:         frontend building
# nodejs:       frontend building
# git:          ./bin/version
# curl:         needed by script that installs Clojure CLI & Lein

RUN 

RUN curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -o /usr/local/bin/lein ; \
    chmod +x /usr/local/bin/lein ; \
    /usr/local/bin/lein upgrade ; \
    curl https://download.clojure.org/install/linux-install-1.11.1.1149.sh -o /tmp/linux-install-1.11.1.1149.sh; \
    chmod +x /tmp/linux-install-1.11.1.1149.sh;\
    sh /tmp/linux-install-1.11.1.1149.sh



RUN curl --silent --location https://rpm.nodesource.com/setup_12.x | bash - ;\
    curl -sL https://dl.yarnpkg.com/rpm/yarn.repo |   tee /etc/yum.repos.d/yarn.repo 

# Add End Point CentOS 7 repo
RUN yum -y install https://packages.endpointdev.com/rhel/7/os/x86_64/endpoint-repo.x86_64.rpm

RUN yum update -y; yum install -y coreutils ttf-dejavu fontconfig bash nodejs yarn git curl openssl ; \
    yum clean all; yum makecache

CMD ["/bin/sh"] 