FROM mizzouceri/tomcat-mvn-java11:V1
LABEL maintainer="Songjie Wang <wangso@missouri.edu>"

# Redirect EOL Debian Buster repositories to archive.debian.org
RUN sed -i -e 's|http://deb.debian.org/debian|http://archive.debian.org/debian|g' \
           -e 's|http://security.debian.org/debian-security|http://archive.debian.org/debian-security|g' \
           -e 's|oldoldstable|buster|g' \
           -e '/buster-updates/d' \
           /etc/apt/sources.list /etc/apt/sources.list.d/* 2>/dev/null || true && \
    apt-get -o Acquire::Check-Valid-Until=false -o Acquire::AllowInsecureRepositories=true -y update && \
    apt-get install -y --no-install-recommends --allow-unauthenticated \
        lsb-release net-tools nano default-mysql-server maven && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/local/tomcat/webapps/ROOT/js
COPY Covid19-website/src/main/resources/static/js/ng-table.js /usr/local/tomcat/webapps/ROOT/js/
WORKDIR /root
ADD Covid19-website /root/Covid19-website

WORKDIR /root/Covid19-website
