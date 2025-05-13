FROM alpine:3.21

ARG PRODUCT="packer"
ARG VERSION="1.12.0"
ARG TERRAFORM_DOCS_VERSION="v0.20.0"

RUN apk update && apk add --no-cache \
    coreutils \
    curl \
    git \
    gnupg \
    grep \
    hcloud \
    kubectl \
    libffi-dev \
    linux-headers \
    musl-dev \
    openssh-client \
    opentofu \
    pre-commit \
    sed \
    tzdata \
    unzip \
    wget \
    which \
    zip

WORKDIR /tmp
# Install and verify packer
RUN wget https://releases.hashicorp.com/${PRODUCT}/${VERSION}/${PRODUCT}_${VERSION}_linux_amd64.zip && \
    wget https://releases.hashicorp.com/${PRODUCT}/${VERSION}/${PRODUCT}_${VERSION}_SHA256SUMS && \
    wget https://releases.hashicorp.com/${PRODUCT}/${VERSION}/${PRODUCT}_${VERSION}_SHA256SUMS.sig && \
    wget -qO- https://www.hashicorp.com/.well-known/pgp-key.txt | gpg --import && \
    gpg --verify ${PRODUCT}_${VERSION}_SHA256SUMS.sig ${PRODUCT}_${VERSION}_SHA256SUMS && \
    grep ${PRODUCT}_${VERSION}_linux_amd64.zip ${PRODUCT}_${VERSION}_SHA256SUMS | sha256sum -c && \
    unzip ${PRODUCT}_${VERSION}_linux_amd64.zip -d /usr/local/bin && \
    chmod +x /usr/local/bin/${PRODUCT}

# Install terraform-docs
RUN curl -Lo /terraform-docs.tar.gz https://github.com/terraform-docs/terraform-docs/releases/download/${TERRAFORM_DOCS_VERSION}/terraform-docs-${TERRAFORM_DOCS_VERSION}-$(uname)-amd64.tar.gz && \
    tar -xzf /terraform-docs.tar.gz -C /usr/local/bin && \
    chmod +x /usr/local/bin/terraform-docs && \
    rm /terraform-docs.tar.gz

WORKDIR /root

RUN git config --global --add safe.directory '*'
