# Run the tests
FROM python:3.9-slim

WORKDIR /app
ARG PIP_EXTRA_INDEX_URL

# Install dependencies
ADD requirements.txt .

RUN apt-get update \
    && apt-get install -y wait-for-it openssh-client sshpass

RUN mkdir -p -m 0600 ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts

RUN --mount=type=ssh,id=ed pip install -r requirements.txt

# Add the app
ADD . .

# Engage.
CMD ["behave", "--no-capture"]
