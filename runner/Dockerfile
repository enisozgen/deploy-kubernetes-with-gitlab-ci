FROM gitlab/gitlab-runner

RUN apt-get update && apt-get install gettext-base sudo docker.io git curl -yq --no-install-recommends

# Allow user to use docker socket
RUN echo "gitlab-runner ALL=(ALL:ALL) NOPASSWD: /usr/bin/docker" > /etc/sudoers
