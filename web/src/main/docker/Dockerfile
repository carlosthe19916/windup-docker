FROM jboss/base-jdk:8

ENV RHAMT_VERSION @version.windup.web@
ENV RHAMT_HOME /opt/jboss/rhamt-web
ENV DOWNLOAD_DIR /home/jboss

USER root

# Add rhamt distribution to /opt/jboss
ADD maven/opt/jboss/rhamt-web $DOWNLOAD_DIR

# Make jboss the owner of the content
RUN cd $DOWNLOAD_DIR \
    && unzip rhamt-web-distribution-${RHAMT_VERSION}-with-authentication.zip \
    && mv ${DOWNLOAD_DIR}/rhamt-web-distribution-${RHAMT_VERSION} $RHAMT_HOME \
    && rm rhamt-web-distribution-${RHAMT_VERSION}-with-authentication.zip \
    && rm -rf ${RHAMT_HOME}/standalone/configuration/standalone_xml_history \
    && chown -R jboss:jboss ${RHAMT_HOME} \
    && chmod -R g+rw ${RHAMT_HOME}

# Ensure signals are forwarded to the JVM process correctly for grateful shutdown
ENV LAUNCH_JBOSS_IN_BACKGROUND true

USER jboss

# Expose the ports we're interesting in
EXPOSE 8080

# Set the default command to run on boot
# This will boot rhamt and bind all interface
CMD ["/opt/jboss/rhamt-web/run_rhamt.sh", "-b", "0.0.0.0"]