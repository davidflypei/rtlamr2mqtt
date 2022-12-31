FROM allangood/rtlamr2mqtt

WORKDIR /go/src/app

FROM python:3.10-slim

COPY ./rtlamr2mqtt.py /usr/bin
COPY ./requirements.txt /tmp
COPY ./sdl_ids.txt /var/lib/

RUN apt-get update \
    && apt-get install -o Dpkg::Options::="--force-confnew" -y \
      libusb-1.0-0 \
    && apt-get --purge autoremove -y \
    && apt-get clean \
    && find /var/lib/apt/lists/ -type f -delete \
    && pip install -r /tmp/requirements.txt \
    && chmod 755 /usr/bin/rtlamr2mqtt.py \
    && rm -rf /usr/share/doc /tmp/requirements.txt

STOPSIGNAL SIGTERM

ENTRYPOINT ["/usr/bin/rtlamr2mqtt.py"]
