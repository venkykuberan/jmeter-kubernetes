# Build and Push jmeter image

To generate jmeter docker image run the following command on this folder

-   docker build -t <namespace>/jmeter:1.0 .

Push the image build from above command to your image repository 

-   docker push <namespace>/jmeter:1.0