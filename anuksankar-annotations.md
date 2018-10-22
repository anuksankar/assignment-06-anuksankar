# W205 - Assignment 6 - Anu Sankar 
 
#### Preliminary Checklist

After logging in to my droplet, I completed the before assignment checklist to remove any stray containers and also update to the latest images.
Then I cloned my assignment-06-anuksankar repo and created a branch anuksankar_hw6_branch for this assignment.  Then I switched to the branch.

  git checkout anuksankar_hw6_branch

I created a directory "kafka" in my branch.
  mkdir kafka

#### Copy docker-compose.yml from course-content directory

  cp ~/w205/course-content/06-Transforming-Data/docker-compose.yml ~/w205/assignment-06-anuksankar/kafka/

#### Changed directory to kafka
  cd kafka

#### Fetch the assignment json file
  
  curl -L -o assessment-attempts-20180128-121051-nested.json https://goo.gl/ME6hjp


#### Spin-up the Cluster

  docker-compose up -d

In another session window, I  verified that the docker-compose.yml file showed three containers: kafka, mids and zookeeper.  Then I also looked at the logs in a third session window.

#### Created a topic

  docker-compose exec kafka kafka-topics --create --topic foo --partitions 1 --replication-factor 1 --if-not-exists --zookeeper zookeeper:32181

I saw the message Created topic "foo".

#### Check the topic

 docker-compose exec kafka kafka-topics --describe --topic foo --zookeeper zookeeper:32181

#### Checkout the messages

 docker-compose exec mids bash -c "cat /w205/assignment-06-anuksankar/kafka/assessment-attempts-20180128-121051-nested.json"

The json file had a lot of data and was very messy to read.  

 docker-compose exec mids bash -c "cat /w205/assignment-06-anuksankar/kafka/assessment-attempts-20180128-121051-nested.json | jq '.'"

Publishing to jq made is easy to read

  docker-compose exec mids bash -c "cat /w205/assignment-06-anuksankar/kafka/assessment-attempts-20180128-121051-nested.json | jq '.[]' -c"

The above command removes the white spaces and compresses the file when publishing to jq.

#### Published messages through kafkacat 

  docker-compose exec mids bash -c "cat /w205/assignment-06-anuksankar/kafka/assessment-attempts-20180128-121051-nested.json | jq '.[]' -c | kafkacat -P -b kafka:29092 -t foo && echo 'Produced 100 messages.'"

#### Consume the messages using kafacat    

docker-compose exec mids bash -c "kafkacat -C -b kafka:29092 -t foo -o beginning -e"

#### Consume only the first 42 messages of the published 100 using kafka console consumer

docker-compose exec kafka kafka-console-consumer --bootstrap-server kafka:29092 --topic foo --from-beginning --max-messages 42

#### I was also able to pipe it into wordcount 

docker-compose exec mids bash -c "kafkacat -C -b kafka:29092 -t foo -o beginning -e" | wc -l

#### Tear down the cluster 

docker-compose down

#### Create a history file

history>anuksankar-history.txt






























