  599  sudo chown -R science:science ~/w205
  600  cd ~/w205/course-content
  601  git pull --all
  602  cd 
  603  docker ps -a
  604  docker rm -f $(docker ps -aq)
  605  docker ps -a
  606  docker pull midsw205/base:latest
  607  docker pull redis
  608  docker pull confluentinc/cp-zookeeper:latest
  609  docker pull confluentinc/cp-kafka:latest
  610  docker pull midsw205/spark-python:0.0.5
  611  cd w205
  612  ls -l
  613  git pull https://github.com/mids-w205-crook/assignment-06-anuksankar.git
  614  git clone https://github.com/mids-w205-crook/assignment-06-anuksankar.git
  615  ls -l
  616  cd assignment-06-anuksankar
  617  cd ~/assignment-04-anuksankar
  618  cd ../assignment-04-anuksankar
  619  ls -l
  620  git branch
  621  cd ../assignment-05-anuksankar
  622  git branch
  623  cd ../assignment-06-anuksankar
  624  ls -l
  625  git branch anuksankar_hw6_branch
  626  git checkout anuksankar_hw6_branch
  627  mkdir kafka
  628  cp ~/w205/course-content/06-Transforming-Data/docker-compose.yml ~/w205/assignment-06-anuksankar/kafka/
  629  ls -l
  630  cd kafka
  631  curl -L -o assessment-attempts-20180128-121051-nested.json https://goo.gl/ME6hjp
  632  ls -l
  633  cd ..
  634  ls -l
  635  git branch
  636  cd assignment-06-anuksankar
  637  git branch
  638  git checkout anuksankar_hw6_branch
  639  cd kafka
  640  ls -l
  641  docker-compose up -d
  642  docker-compose exec kafka kafka-topics --create --topic foo --partitions 1 --replication-factor 1 --if-not-exists --zookeeper zookeeper:32181
  643  docker-compose exec kafka kafka-topics --describe --topic foo --zookeeper zookeeper:32181
  644  docker-compose exec mids bash -c "cat /w205/assignment-06-anuksankar/kafka/assessment-attempts-20180128-121051-nested.json"
  645  docker-compose exec mids bash -c "cat /w205/assignment-06-anuksankar/kafka/assessment-attempts-20180128-121051-nested.json | jq '.'"
  646  docker-compose exec mids bash -c "cat /w205/assignment-06-anuksankar/kafka/assessment-attempts-20180128-121051-nested.json | jq '.[]' -c"
  647  docker-compose exec mids bash -c "cat /w205/assignment-06-anuksankar/kafka/assessment-attempts-20180128-121051-nested.json | jq '.[]' -c | kafkacat -P -b kafka:29092 -t foo && echo 'Produced 100 messages.'"
  648  docker-compose exec mids bash -c "kafkacat -C -b kafka:29092 -t foo -o beginning -e"
  649  docker-compose exec kafka kafka-console-consumer --bootstrap-server kafka:29092 --topic foo --from-beginning --max-messages 42
  650  docker-compose exec mids bash -c "kafkacat -C -b kafka:29092 -t foo -o beginning -e" | wc -l
  651  docker-compose down
  652  history> history.txt
