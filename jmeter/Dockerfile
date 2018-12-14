# Use Alpine
FROM alpine
MAINTAINER VenkyKuberan

# Install wget & JRE
RUN apk upgrade --update && \
	apk add wget openjdk7-jre unzip 
 
# Install jmeter
RUN   mkdir /jmeter \
	&& cd /jmeter/ \
	&& wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-2.13.tgz \
	&& tar -xzf apache-jmeter-2.13.tgz \
	&& rm apache-jmeter-2.13.tgz \
	&& mkdir /jmeter-plugins \
	&& cd /jmeter-plugins/ \
	&& wget https://jmeter-plugins.org/downloads/file/JMeterPlugins-ExtrasLibs-1.4.0.zip \
	&& unzip -o JMeterPlugins-ExtrasLibs-1.4.0.zip -d /jmeter/apache-jmeter-2.13/

RUN mkdir /jmeter/apache-jmeter-2.13/scripts \
	&& mkdir /jmeter/apache-jmeter-2.13/results

ENV SCRIPT_NAME sampletest.jmx	

COPY $SCRIPT_NAME /jmeter/apache-jmeter-2.13/scripts

# Set Jmeter Home
ENV JMETER_HOME /jmeter/apache-jmeter-2.13
ENV SCRIPTS_FOLDER $JMETER_HOME/scripts
ENV RESULTS_FOLDER $JMETER_HOME/results

# Add Jmeter to the Path
ENV PATH $JMETER_HOME/bin:$PATH

ENTRYPOINT $JMETER_HOME/bin/jmeter -Jjmeter.save.saveservice.print_field_names=true -Jduration=$duration -n -t=$SCRIPTS_FOLDER/$SCRIPT_NAME -l=$RESULTS_FOLDER/test_results.csv