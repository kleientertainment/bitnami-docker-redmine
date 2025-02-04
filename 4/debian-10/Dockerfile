FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV PATH="/opt/bitnami/ruby/bin:/opt/bitnami/postgresql/bin:/opt/bitnami/mysql/bin:/opt/bitnami/git/bin:/opt/bitnami/common/bin:/opt/bitnami/nami/bin:$PATH"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl ghostscript gsfonts gzip imagemagick libaudit1 libbsd0 libc6 libcap-ng0 libcom-err2 libcurl4 libedit2 libffi6 libgcc1 libgcrypt20 libgmp-dev libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libicu63 libidn2-0 libjemalloc2 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 liblzma5 libmariadb3 libncurses6 libnettle6 libnghttp2-14 libp11-kit0 libpam0g libpq5 libpsl5 libreadline-dev libreadline7 librtmp1 libsasl2-2 libssh2-1 libssl-dev libssl1.1 libstdc++6 libtasn1-6 libtinfo6 libunistring2 libuuid1 libxml2 libxml2-dev libxslt1-dev libxslt1.1 procps sqlite3 sudo tar zlib1g zlib1g-dev
RUN /build/bitnami-user.sh
RUN /build/install-nami.sh
RUN bitnami-pkg install ruby-2.6.7-0 --checksum 3d605c181d6ae44f6a6debb7c89a4dc64081b5ee28ca41354946f1fa5cd1276a
RUN bitnami-pkg install postgresql-client-11.12.0-0 --checksum 94395af20a0ee9e12aaab0d1a58bb42290145af8ab7f736c4bb7cc3f51bbf2b6
RUN bitnami-pkg install mysql-client-10.3.30-0 --checksum 47107f86621bb184307e47bbb15244d076575f0e0f7d339f198ef312b6f3f285
RUN bitnami-pkg install git-2.32.0-0 --checksum 3094f50c904e966bd6c6a2d6152cf41fd3a816d32395622a785ccbcda62b7c5f
RUN bitnami-pkg install tini-0.19.0-1 --checksum 9b1f1c095944bac88a62c1b63f3bff1bb123aa7ccd371c908c0e5b41cec2528d
RUN bitnami-pkg unpack redmine-4.2.1-0 --checksum 48c132cf0dea75627e33be6c8d983b13bbba4d49d528f5e1669c6da51f3865ef
RUN bitnami-pkg install gosu-1.13.0-0 --checksum fd7257c2736164d02832dbf72e2c1ed9d875bf3e32f0988520796bc503330129

COPY rootfs /
ENV BITNAMI_APP_NAME="redmine" \
    BITNAMI_IMAGE_VERSION="4.2.1-debian-10-r56" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux" \
    REDMINE_DB_MYSQL="mariadb" \
    REDMINE_DB_NAME="bitnami_redmine" \
    REDMINE_DB_PASSWORD="" \
    REDMINE_DB_PORT_NUMBER="" \
    REDMINE_DB_POSTGRES="" \
    REDMINE_DB_USERNAME="bn_redmine" \
    REDMINE_EMAIL="user@example.com" \
    REDMINE_LANGUAGE="en" \
    REDMINE_PASSWORD="bitnami1" \
    REDMINE_USERNAME="user" \
    SMTP_AUTHENTICATION="login" \
    SMTP_DOMAIN="example.com" \
    SMTP_HOST="" \
    SMTP_PASSWORD="" \
    SMTP_PORT="" \
    SMTP_TLS="true" \
    SMTP_USER="" \
    RAILS_ENV=production

RUN apt update && apt install -y build-essential
RUN cd /opt/bitnami/redmine/plugins && git clone https://github.com/twinslash/redmine_omniauth_google.git
RUN cd /opt/bitnami/redmine && bundle config unset deployment && bundle install

EXPOSE 3000

ENTRYPOINT [ "/app-entrypoint.sh" ]
CMD [ "/run.sh" ]
