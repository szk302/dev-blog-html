ARG ASCIIDOCTOR_VERSION='1.14.0'

FROM asciidoctor/docker-asciidoctor:"${ASCIIDOCTOR_VERSION}"

ARG HUGO_VERSION='0.80.0'

ENV HUGO_BASE_URL="https://github.com/gohugoio/hugo/releases/download"
ENV HUGO_TAR_FILE_NAME="hugo_extended_${HUGO_VERSION}_Linux-64bit.tar.gz"
ENV HUGO_TAR_FILE_URL="${HUGO_BASE_URL}/v${HUGO_VERSION}/${HUGO_TAR_FILE_NAME}"
ENV HUGO_CHECKSUM_URL="${HUGO_BASE_URL}/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_checksums.txt"

WORKDIR /tmp/work
SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

# Hugoのインストール
RUN apk add --no-cache \
    git \
    ca-certificates \
    libc6-compat \
    libstdc++ && \
    curl -LO "${HUGO_TAR_FILE_URL}" && \
    curl -LO "${HUGO_CHECKSUM_URL}" && \
    grep "${HUGO_TAR_FILE_URL##*/}" "./${HUGO_CHECKSUM_URL##*/}" | sha256sum -c - && \
    tar -zxvf "${HUGO_TAR_FILE_URL##*/}" && \
    mv ./hugo /usr/bin/hugo && \
    rm -rf /tmp/work/*

# PlantUML使用するための拡張/依存モジュールの追加
RUN apk add --no-cache ruby-dev alpine-sdk graphviz
RUN gem install bundler json asciidoctor-html5s asciidoctor-diagram