
# jmeter-kubernetes

The project is to setup load generators on kubernetes to run a load test against any APIs/Systems.

# Getting Started
These instructions will get you setup kuebernetes pods with jmeter and filebeat containers to load test against your api or application.

# Prerequisites
* jmeter (dockerized) - Load injectors
* filebeat (dockerized) - to collect and ship jmeter logs/results
* elasticsearch (AWS service) - data store, dashboards and visualization for performance test results
* kubernetes cluster- load test enviroment to execute the test
* [kubectl] (https://kubernetes.io/docs/tasks/tools/install-kubectl/) - Kuberenetes cli tool


# Installation/Setup
 - jmeter -- Run the docker file under jmeter folder and push it to AWS ECS (you can push it any docker repo like dockerhub.com but make sure you give the right address of your image in jmeter-job.yml)

 - filebeat -- Run the docker file under filbeat folder and push it to AWS ECS (you can push it any docker repo like dockerhub.com but make sure you give the right address of your image in jmeter-job.yml)

 - kubernetes -- Create a kubernetes cluster for your team. Reach out to your Kubernetes team if you have one for your namespace in the cluster

 - elasticsearch 
    * Run the cloudformation template under elasticsearch/cloudformation folder in AWS Console or using AWS cli to create elasticsearch template. Make sure you use your team's account
        in the line "ESResource":"arn:aws:es:us-west-2:**your-team-account**:domain/**your-cluster-name**-*/*"


    * In postman or curl, run the put command against your elasticsearch cluster https://**your-elasticsearch-url**.us-west-2.es.amazonaws.com/_ingest/pipeline/parsejmetercsv with the contents in elasticsearch/ingestpipeline.json file. This is to make elasticsearch to consider the fields of jmeter results while creating the records/documents

# Running the tests
kubectl create -f jmeter-job.yml

# Scaling the load
kubectl scale --replicas=3 jobs/**job_name**

example - kubectl scale --replicas=1 jobs/jmeter-client-load

# Clean up
After the test is over you can delete the job to have a clean start for the next test

kubectl delete job **job_name**



