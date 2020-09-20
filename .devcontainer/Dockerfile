# Uncomment one of the following lines to select the SDK variant

# Variant 1: Open-Source PlayStation 2 SDK
#FROM ps2ded-oss

# Variant 2: Sony PlayStation 2 SDK
FROM ps2ded-sce

# Install common packages
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive && \
    apt-get -y install --no-install-recommends \
        ca-certificates \
        git

# Handle workaround for Windows volumes
RUN mkdir -p /root/work