# Based on the proof of concept using Divolte, Kafka, Druid and Superset:
Please refer to the blogpost for more information: https://blog.godatadriven.com/divolte-kafka-druid-superset

The current example was not working for me so made some updates to run on my local machine which is running Ubuntu 20.04
Had to use network mode for pretty much every container to get this work which I am sure is not best practice.
May review how to close these extra ports and get this example working as originally intended again.

# Changes:
1. Pretty much all containers in docker-compose use network: "host" so that I can just use localhost to connect everything
2. Manually building the image for the druid container in docker-compose using the Docker image defined in the github link: https://github.com/Fokko/docker-druid
3. Made the druid container the first build in docker-compose to allow for its zookeeper instance to be used by Kafka
4. Changed supervisor-spec.json to use localhost
5. Updated app/index.html to add http:// to find divolte url locally
6. Changed app port to 8095 to prevent conflict with port 8090 orignally used in example, but which conflicts with port in https://github.com/Fokko/docker-druid
7. Added additional images to HTML page and type field to Divolte
8. Running in an EC2: 
* Need an EC2 with at least 4 cores and need to set Inbound Rules for all ports (8888,8088,8095,9092,8081,8082)
* Set url for index.html site to IPv4 of EC2 to allow for Divolte to Kafka interoperability
