FROM jenkins/inbound-agent:jdk21

USER root

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv \
    curl \
    unzip

# Добавляем known_hosts для github.com (чтобы не было запроса на подтверждение ключа при первом подключении)
RUN mkdir -p /home/jenkins/.ssh && \
    chmod 700 /home/jenkins/.ssh && \
    ssh-keyscan -t rsa,ecdsa,ed25519 github.com > /home/jenkins/.ssh/known_hosts && \
    chmod 644 /home/jenkins/.ssh/known_hosts && \
    chown -R jenkins:jenkins /home/jenkins/.ssh

# создаём виртуальное окружение
RUN python3 -m venv /opt/venv

# активируем venv и устанавливаем нужные пакеты
RUN /opt/venv/bin/pip install --upgrade pip \
    && curl -o allure.zip -L https://github.com/allure-framework/allure2/releases/download/2.35.1/allure-2.35.1.zip \
    && unzip allure.zip -d /opt/ \
    && ln -s /opt/allure-2.35.1/bin/allure /usr/bin/allure \
    && rm allure.zip

# экспортируем PATH, чтобы везде использовался venv
ENV PATH="/opt/venv/bin:$PATH"

RUN python --version && pip --version && allure --version

USER jenkins
