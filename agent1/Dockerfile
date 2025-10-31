FROM jenkins/inbound-agent:jdk21

USER root

# Установка Docker CLI
RUN apt-get update && \
    apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && \
    apt-get install -y docker-ce-cli

# Добавляем known_hosts для github.com (чтобы не было запроса на подтверждение ключа при первом подключении)
RUN mkdir -p /home/jenkins/.ssh && \
    chmod 700 /home/jenkins/.ssh && \
    ssh-keyscan -t rsa,ecdsa,ed25519 github.com > /home/jenkins/.ssh/known_hosts && \
    chmod 644 /home/jenkins/.ssh/known_hosts && \
    chown -R jenkins:jenkins /home/jenkins/.ssh

USER jenkins