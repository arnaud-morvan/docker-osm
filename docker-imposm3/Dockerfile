FROM golang:1.6
MAINTAINER Etienne Trimaille <etienne@kartoza.com>

RUN apt-get update && apt-get install -y python-pip \
      libprotobuf-dev libleveldb-dev libgeos-dev \
      libpq-dev python-dev postgresql-client-9.4 \
      --no-install-recommends

RUN ln -s /usr/lib/libgeos_c.so /usr/lib/libgeos.so

WORKDIR $GOPATH
RUN go get github.com/omniscale/imposm3
RUN cd /go/src/github.com/omniscale/imposm3 && git checkout c90badc
RUN go install github.com/omniscale/imposm3

ADD requirements.txt /home/requirements.txt
RUN pip install -r /home/requirements.txt

ADD importer.py /home/

WORKDIR /home
CMD ["bash", "-c", "python -u /home/importer.py || sleep 3600"]
