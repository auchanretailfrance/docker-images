FROM postgres:11.9


RUN apt-get update \
  && apt-get install -y curl \
  && curl https://install.citusdata.com/community/deb.sh | bash \
  && apt-get install -y postgresql-11-auto-failover-1.3 \
  && /usr/bin/pg_autoctl --version \
  && rm -rf /var/lib/apt/lists/*
