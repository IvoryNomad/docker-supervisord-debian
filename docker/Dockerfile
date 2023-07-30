FROM debian:bookworm-slim

RUN <<EOT /bin/bash
    apt-get update
    apt-get upgrade -y
    apt-get install --no-install-recommends -y \
        supervisor
    apt-get remove -y make gcc git wget gettext
    apt-get autoremove -y
    apt-get clean
    rm -rf /var/lib/apt/lists/*
    rm -rf /var/cache/* /var/log/* /tmp/* /var/lib/dpkg/status-old
    mkdir /entrypoint.d
EOT

COPY ./files/config/supervisord.conf /etc/supervisor 
COPY ./files/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
VOLUME [ "/etc/supervisor", "/var/log/supervisor" ]
ENTRYPOINT [ "/entrypoint.sh" ]
