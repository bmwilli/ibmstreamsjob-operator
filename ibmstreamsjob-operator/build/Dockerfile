FROM docker.io/bmwilli1/streams-jmx-client:5 AS builder
FROM quay.io/operator-framework/ansible-operator:v0.17.0

# Install Java to run streams-jmx-client
USER root
RUN yum -y install java-1.8.0-openjdk

ENV JAVA_HOME /usr/

# copy streams-jmx-client too from builder image
COPY --from=builder /executable-streams-jmx-client.jar .

COPY requirements.yml ${HOME}/requirements.yml
RUN ansible-galaxy collection install -vvv -r ${HOME}/requirements.yml \
 && chmod -R ug+rwx ${HOME}/.ansible 

COPY watches.yaml ${HOME}/watches.yaml

COPY roles/ ${HOME}/roles/
COPY playbooks/ ${HOME}/playbooks/
