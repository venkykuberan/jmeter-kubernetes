# Build and Push filebeat image

To generate jmeter docker image run the following command on this folder

-   docker build -t <namespace>/filbeat:1.0 .

Push the image build from the above command to your image repository 

-   docker push <namespace>/filebeat:1.0