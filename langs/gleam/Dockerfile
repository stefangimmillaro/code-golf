FROM alpine:3.20 AS builder

RUN apk add --no-cache curl erlang

RUN curl -L https://github.com/gleam-lang/gleam/releases/download/v1.2.1/gleam-v1.2.1-x86_64-unknown-linux-musl.tar.gz | tar xz

RUN mv /gleam /gleam-bin

FROM codegolf/lang-base

COPY --from=0 / /
COPY --from=0 /bin /bin
COPY --from=0 /gleam-bin /usr/bin/gleam
COPY --from=0 /lib/ld-musl-x86_64.so.1 /lib/

COPY gleamwrapper /usr/bin/

# Deps download writes to ~/.cache. /tmp isn't o+write (for some reason).
RUN chmod 777 /tmp

USER nobody

COPY --chown=nobody gleam.toml /gleam/

WORKDIR /gleam

RUN HOME=/tmp gleam deps download

ENTRYPOINT ["gleamwrapper"]

CMD ["--version"]
