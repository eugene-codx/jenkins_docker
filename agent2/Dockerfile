FROM jenkins/inbound-agent:jdk21

USER root

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv \
    curl \
    unzip

# создаём виртуальное окружение
RUN python3 -m venv /opt/venv

# активируем venv и устанавливаем нужные пакеты
RUN /opt/venv/bin/pip install --upgrade pip \
    && curl -o allure.zip -L https://github.com/allure-framework/allure2/releases/latest/download/allure-2.34.0.zip \
    && unzip allure.zip -d /opt/ \
    && ln -s /opt/allure-2.34.0/bin/allure /usr/bin/allure \
    && rm allure.zip

# экспортируем PATH, чтобы везде использовался venv
ENV PATH="/opt/venv/bin:$PATH"

RUN python --version && pip --version && allure --version

USER jenkins
