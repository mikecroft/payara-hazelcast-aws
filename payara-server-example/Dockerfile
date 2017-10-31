FROM payara/server-full

COPY hazelcast-aws-2.1.0.jar ${PAYARA_PATH}/glassfish/domains/${PAYARA_DOMAIN}/lib/ext
COPY rest-jcache-1.0-SNAPSHOT.war ${AUTODEPLOY_DIR}
COPY hazelcast.xml .

RUN echo 'set-hazelcast-configuration --enabled true --dynamic true -f hazelcast.xml' >> ${DEPLOY_COMMANDS}

ENTRYPOINT ${PAYARA_PATH}/generate_deploy_commands.sh && ${PAYARA_PATH}/bin/asadmin start-domain -v --postbootcommandfile ${DEPLOY_COMMANDS} ${PAYARA_DOMAIN}
