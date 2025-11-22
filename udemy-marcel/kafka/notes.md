Stream api – take data from kafka ,performs some operation and puts data back to kafka
Connect api – takes/give   data from ext source and work with kafka and do some operation
1)	Setup kafka
2)	https://github.com/dilipsundarraj1/kafka-for-developers-using-spring-boot-v2/blob/main/SetUpKafkaDocker.md#set-up-broker-and-zookeeper

<img width="648" height="418" alt="image" src="https://github.com/user-attachments/assets/b6e52e10-f283-4a76-9be5-042f48c000e8" />


Send with key sepearor ‘-‘

<img width="854" height="489" alt="image" src="https://github.com/user-attachments/assets/d17000f1-6a7d-4914-b6aa-b9a317b7edd7" />


Consimeroffset topic created automatically by kafka cluster to maintain consumer offset
Partitioner-assign to partition
Record batch when gets full then msg is sent to topic
