FROM ghcr.io/jaumebarber/tofu-kube-hetzner:latest

# Final-stage-specific tools only
RUN apk update && apk add --no-cache \
zsh \
eza \
fd \
openjdk21-jre \
the_silver_searcher

  
# Final touch
RUN git config --global --add safe.directory '*'
  