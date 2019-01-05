FROM dtzar/helm-kubectl:2.12.1

COPY Dockerfile /cnab/Dockerfile
COPY app /cnab/app
COPY kgi /usr/bin
RUN ls -lath /cnab/app/
RUN kgi --help
CMD ["/cnab/app/run"]
