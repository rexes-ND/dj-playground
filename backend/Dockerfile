FROM python:3.10.14-slim-bookworm

# Source: https://github.com/rexes-ND/digit-recognizer/blob/main/backend/Dockerfile
RUN groupadd --gid 1000 rexes \
    && useradd --uid 1000 --gid 1000 -m rexes \
    && apt-get update \
    && apt-get install -y sudo \
    && echo rexes ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/rexes \
    && chmod 0440 /etc/sudoers.d/rexes

USER rexes

WORKDIR /home/rexes/backend

RUN python3 -m venv /home/rexes/venv
ENV PATH="/home/rexes/venv/bin:$PATH"

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

ENV PYTHONUNBUFFERED=1

CMD sudo chmod +x entrypoint.sh && ./entrypoint.sh

EXPOSE 8000
