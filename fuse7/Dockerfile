FROM jbossacr.azurecr.io/jboss-fuse-7-tech-preview/fuse-eap-openshift:v1
MAINTAINER Kuldeep Sharma ..
#Handle Property Files
COPY test1.properties $JBOSS_HOME/properties/
COPY test2.properties $JBOSS_HOME/properties/
RUN   if [ -d $JBOSS_HOME/properties ]; then for propfile in $(find "$JBOSS_HOME/properties/" -type f -size +0 -name "*.properties"); do  JBOSS_PROP="$JBOSS_PROP -P="${propfile}"" ; done;  fi \
        && echo $JBOSS_PROP \
        && echo "export JBOSS_PROPS=\"${JBOSS_PROP}\"" >> ~/.bashrc
ENV PRESERVE_JAVA_OPTS=false
ENV JAVA_OPTS="$JAVA_OPTS -Xmx1024m -Xms1024m -XX:MaxMetaspaceSize=256m -Djava.net.preferIPv4Stack=true -Djboss.modules.system.pkgs=$JBOSS_MODULES_SYSTEM_PKGS -Djava.awt.headless=true"
ENTRYPOINT source ~/.bashrc && /opt/eap/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0 $JBOSS_PROPS
