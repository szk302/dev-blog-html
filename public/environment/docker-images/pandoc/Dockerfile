ARG ASCIIDOCTOR_VERSION='1.14.0'
ARG PANDOC_VERSION='2.16.2'

FROM pandoc/core:${PANDOC_VERSION} as pandoc

FROM asciidoctor/docker-asciidoctor:"${ASCIIDOCTOR_VERSION}"
WORKDIR /tmp/work
SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

COPY --from=pandoc \
  /usr/local/bin/pandoc \
  /usr/local/bin/pandoc-citeproc \
  /usr/local/bin/

RUN apk --no-cache add \
        # pandocの依存モジュール
        gmp \
        libffi \
        lua5.3 \
        lua5.3-lpeg \
        # confulence投入に必要なモジュール
        coreutils \
        jq