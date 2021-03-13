# AWS Cheetsheet

- AWS DynamoDB
  - connect to local endpoint `aws dynamodb list-tables --endpoint-url http://localhost:8000`
  - docker-compose.yml
    ```
    version: '3.8'
      services:
        dynamodb-local:
          command: "-jar DynamoDBLocal.jar -sharedDb -optimizeDbBeforeStartup -dbPath ./data"
          image: "amazon/dynamodb-local:latest"
          container_name: dynamodb-local
          ports:
            - "8000:8000"
          volumes:
            - "./docker/dynamodb:/home/dynamodblocal/data"
          working_dir: /home/dynamodblocal
    ```

## Reference
- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.DownloadingAndRunning.html
