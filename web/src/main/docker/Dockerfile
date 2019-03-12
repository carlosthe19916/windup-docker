FROM jboss/base-jdk:11

ENV RHAMT_HOME /opt/jboss/rhamt-web

USER root

# Add rhamt distribution to /opt/jboss
ADD maven/opt/jboss/rhamt-web ${RHAMT_HOME}

# Make jboss the owner of the content
RUN cd $HOME  \
    && chown -R jboss:0 ${RHAMT_HOME}  \
    && chmod -R g+rw ${RHAMT_HOME}

# Ensure signals are forwarded to the JVM process correctly for grateful shutdown
ENV LAUNCH_JBOSS_IN_BACKGROUND true

USER jboss

# Expose the ports we're interesting in
EXPOSE 8080

# Set the default command to run on boot
# This will boot rhamt and bind all interface
CMD ["/opt/jboss/rhamt-web/run_rhamt.sh", "-b", "0.0.0.0"]