FROM roribio16/alpine-sqs:latest

COPY elasticmq.conf /opt/
COPY logback.xml /opt/
COPY supervisord.conf /etc/supervisor/conf.d/elasticmq.conf

# !!! TODO may need this to disable web interface if container is freaking out
#RUN rm /etc/supervisor/conf.d/insight.conf
