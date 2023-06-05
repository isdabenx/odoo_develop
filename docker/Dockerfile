FROM debian:buster-slim

SHELL ["/bin/bash", "-xo", "pipefail", "-c"]

ENV LANG C.UTF-8

WORKDIR /odoo

RUN apt-get update \
        && apt-get install -y --no-install-recommends ca-certificates curl dirmngr fonts-noto-cjk gnupg libssl-dev \
            node-less npm python3-num2words python3-pip python3-phonenumbers python3-pyldap python3-qrcode \
            python3-renderpm python3-vobject python3-watchdog python3-xlwt xz-utils \
        && curl -o wkhtmltox.deb -sSL https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb \
        && echo '7e35a63f9db14f93ec7feeb0fce76b30c08f2057 wkhtmltox.deb' | sha1sum -c - \
        && apt-get install -y --no-install-recommends ./wkhtmltox.deb \
        && rm -rf /var/lib/apt/lists/* wkhtmltox.deb

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ buster-pgdg main' > /etc/apt/sources.list.d/pgdg.list \
        && export GNUPGHOME="$(mktemp -d)" \
        && repokey='B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8' \
        && gpg --batch --keyserver keyserver.ubuntu.com --recv-keys "${repokey}" \
        && gpg --batch --armor --export "${repokey}" > /etc/apt/trusted.gpg.d/pgdg.gpg.asc \
        && gpgconf --kill all \
        && rm -rf "$GNUPGHOME" \
        && apt-get update  \
        && apt-get install -y postgresql-client \
        && rm -rf /var/lib/apt/lists/*

RUN npm install -g rtlcss

RUN adduser --system --quiet --shell=/bin/bash --home=/odoo --gecos 'ODOO' --group odoo
RUN adduser odoo sudo

RUN apt-get update && apt-get install -y libtool python3-dev libffi-dev libxml2-dev libxslt1-dev zlib1g-dev autoconf \
        python3-wheel libevent-dev git procps libpq-dev libcairo2 libcairo2-dev

COPY ./requirements.txt requirements.txt
RUN pip3 install --upgrade pip \
        && pip3 install -r requirements.txt \
        && rm requirements.txt

VOLUME [ "/mnt", "/odoo" ]

EXPOSE 8069 8072

USER odoo

CMD ["/bin/bash", "-c", "while true; do sleep 1000; done"]