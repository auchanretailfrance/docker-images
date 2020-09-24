FROM postgres:12.4


RUN apt-get update \
  && apt-get install -y curl \
  && curl https://install.citusdata.com/community/deb.sh | bash \
  && apt-get install -y postgresql-12-auto-failover-1.4 \
  && /usr/bin/pg_autoctl --version \
  && rm -rf /var/lib/apt/lists/*
