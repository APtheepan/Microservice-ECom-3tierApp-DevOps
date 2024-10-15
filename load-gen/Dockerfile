FROM python:3.9 as base

WORKDIR /load

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY entrypoint.sh /load
COPY robot-shop.py /load
COPY load-gen.sh /load


FROM debian:bullseye-slim as bash

# Install Python and bash
RUN apt-get update && \
    apt-get install -y python3 python3-pip bash && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

#Get distroless image
FROM gcr.io/distroless/base

ENV HOST="http://localhost:8080/" \
    SILENT=0 \
    NUM_CLIENTS=1 \
    ERROR=0 \
    RUN_TIME=0


COPY --from=base /load .
COPY --from=bash /bin/bash /bin/bash
#RUN chmod +x /bin/bash
# This one doesn't work when it's come to python distroless image
# Because it tries to run the bash script as the python script,
# so, we have to explicitly run the bash script with /bin/bash

CMD ["/bin/bash","entrypoint.sh"]


