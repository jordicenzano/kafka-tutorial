# KAFKA TUTORIAL
The idea of this repo is to provide some simple step by step guide to set up a an isolated test/dev version Kafka locally and start playing around with it :-).
This set up is totally NOT recommended for production workloads.

Note: As I mentioned in [References](#References) this work is based in the containers build by [wurstmeister](https://github.com/wurstmeister)

## Set up Kafka locally (isolated)
Because our purpose is just to experiment, to accelerate the set up we could use a docker images (to be accurate, docker-compose).
First of all we need to clone this repo:
```
git clone git@github.com:jordicenzano/kafka-tutorial.git
cd kafka-tutorial
```

The first step is to pull the docker images and start the cluster based on those images.
To do that we'll execute the following command **from the root of this project**(*):
```
docker-compose up 
```
Remember the 1st time you will call that it will take a while because it needs to download the docker images.
(*) We are assuming that you have docker installed and configured, if not take a look to this [guide](https://docs.docker.com/install/overview/)

### Testing Kafka messaging
We'll test Kafka from inside the Kafka container, to do that we need to open a shell there executing:
```
docker-compose exec kafka bash
```

Now from that shell we can add messages to the topic `test` by doing:
```
# cd $KAFKA_HOME
# bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
> Hello!
```

We can open another shell to receive (consume) those messages from that `test` topic executing the following commands:
```
# cd $KAFKA_HOME
# bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```
Now we should see all the messages sent to `test` from the beginning, also the new ones on the console.

### Clean up
Stop the docker containers by doing:
```
docker-compose down
```

## References
- Deploying a Kafka broker in a Docker container: https://www.kaaproject.org/kafka-docker
- Kafka docker: https://github.com/wurstmeister/kafka-docker
