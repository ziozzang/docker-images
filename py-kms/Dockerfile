FROM debian

RUN apt-get update && apt-get install -fy git-core python && cd / && git clone https://github.com/kz26/py-kms

EXPOSE 1688
CMD ["/usr/bin/python", "/py-kms/server.py"]
