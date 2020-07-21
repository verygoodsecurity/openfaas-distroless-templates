FROM openfaas/classic-watchdog:0.18.1 as watchdog

FROM debian:buster-slim AS build
RUN apt-get update && \
    apt-get install --no-install-suggests --no-install-recommends --yes python3-venv gcc libpython3-dev && \
    python3 -m venv /venv && \
    /venv/bin/pip install --upgrade pip

# Build the virtualenv as a separate step: Only re-execute this step when requirements.txt changes
FROM build AS build-venv
COPY requirements.txt /general_requirements.txt
COPY function/requirements.txt /function_requirements.txt
RUN /venv/bin/pip install --disable-pip-version-check -r /general_requirements.txt
RUN /venv/bin/pip install --disable-pip-version-check -r /function_requirements.txt

# Copy the virtualenv into a distroless image
FROM gcr.io/distroless/python3-debian10:debug
WORKDIR /home/nobody/
USER nobody

COPY --from=build-venv /venv /venv
COPY --from=watchdog /fwatchdog .
COPY index.py .
COPY function function

ENV fprocess="/venv/bin/python3 index.py"
EXPOSE 8080

HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1

ENTRYPOINT ["./fwatchdog"]
