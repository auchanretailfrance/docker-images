FROM postgres:12 AS builder


RUN apt-get update \
  && apt-get install -y \
    build-essential \
    git \
    postgresql-server-dev-12 \
    libicu-dev \
    libkrb5-dev \
    libssl-dev \
    libedit-dev \
    libpam-dev \
    zlib1g-dev \
    libxml2-dev \
    libxslt1-dev \
    libselinux1-dev \    
  && rm -rf /var/lib/apt/lists/*

RUN cd /tmp \
  && git clone https://github.com/citusdata/pg_auto_failover.git

WORKDIR /tmp/pg_auto_failover
RUN make
RUN make install

FROM postgres:12

COPY --from=builder /usr/lib/postgresql/12/bin/pg_autoctl /usr/lib/postgresql/12/bin/pg_autoctl
RUN ln -s /usr/lib/postgresql/12/bin/pg_autoctl /usr/local/bin/pg_autoctl
COPY --from=builder /usr/lib/postgresql/12/lib/pgautofailover.so /usr/lib/postgresql/12/lib/pgautofailover.so
COPY --from=builder /usr/lib/postgresql/12/lib/bitcode/pgautofailover.index.bc /usr/lib/postgresql/12/lib/bitcode/pgautofailover.index.bc
COPY --from=builder /usr/lib/postgresql/12/lib/bitcode/pgautofailover /usr/lib/postgresql/12/lib/bitcode/pgautofailover
COPY --from=builder /usr/share/postgresql/12/extension/pgautofailover* /usr/share/postgresql/12/extension/

