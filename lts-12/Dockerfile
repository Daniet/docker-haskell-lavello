FROM fpco/stack-build:lts-12.21

# Make new user, make it passwordless sudo
RUN useradd -d /home/ubuntu -ms /bin/bash -g root -G sudo -p ubuntu ubuntu
RUN echo "ubuntu ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/ubuntu
USER ubuntu
WORKDIR /home/ubuntu

# Build Haskell dependencies that we use
RUN stack build --resolver lts-12.21 \
  dhall-1.21.0 dhall-json-1.2.7 megaparsec-7.0.3 repline-0.2.0.0 serialise-0.2.1.0 dotgen-0.4.2 cborg-json-0.2.1.0 versions-3.5.0 \
  text turtle filepath file-embed aeson aeson-pretty containers \
  bytestring prettyprinter async-pool process network-uri github lens \
  safe fsnotify Glob async stm directory mtl exceptions unliftio \
  http-client http-client-tls basement zlib tls transformers-base unliftio-core

# Install nix
USER root
RUN  mkdir -p /nix /etc/nix && chmod a+rwx /nix && echo 'sandbox = false' > /etc/nix/nix.conf
USER ubuntu
SHELL ["/bin/bash", "-c"]
ENV USER=ubuntu
RUN touch .bash_profile && curl https://nixos.org/releases/nix/nix-2.2.2/install | sh
RUN source /home/ubuntu/.nix-profile/etc/profile.d/nix.sh
