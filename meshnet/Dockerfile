FROM ghcr.io/home-assistant/amd64-base-debian:latest

# Set non-interactive mode to avoid prompting
ARG DEBIAN_FRONTEND=noninteractive

# From NordVPN install instructions
RUN yes y | sh <(curl -sSf https://downloads.nordcdn.com/apps/linux/install.sh) || true

# Clean-up in ile 5
RUN apt-get autoremove -y
RUN apt-get autoclean -y
RUN rm -rf /var/lib/apt/lists/* /tmp/*

# From MaxWinterSteins Home-assistant Addons
# add the options.json to environment variable magic
COPY export-env-from-config.sh /export-env-from-config.sh

# Copy scripts from MattsTechInfo
COPY /fs /
CMD chmod 755 /etc/cont-init.d/*

ENV S6_CMD_WAIT_FOR_SERVICES=1
CMD nordvpn_login && meshnet_config && meshnet_watch
