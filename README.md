## Run

cd ~/environment/unicorn-spring-ai-agent
export SPRING_DATASOURCE_URL=$(aws ssm get-parameter --name unicornstore-db-connection-string \
  | jq --raw-output '.Parameter.Value')
export SPRING_DATASOURCE_PASSWORD=$(aws secretsmanager get-secret-value --secret-id unicornstore-db-secret \
  | jq --raw-output '.SecretString' | jq -r .password)
./mvnw spring-boot:run

## Commands


### Local memory
cd ~/environment/unicorn-spring-ai-agent
./mvnw spring-boot:run

### External memory
cd ~/environment/unicorn-spring-ai-agent
export SPRING_DATASOURCE_URL=$(aws ssm get-parameter --name unicornstore-db-connection-string \
  | jq --raw-output '.Parameter.Value')
export SPRING_DATASOURCE_PASSWORD=$(aws secretsmanager get-secret-value --secret-id unicornstore-db-secret \
  | jq --raw-output '.SecretString' | jq -r .password)
./mvnw spring-boot:run

### RAG with PGvector
curl -X POST \
-H "Content-Type: text/plain" \
-d "Unicorn have origins in different cultures: Chinese Qilin, Indian unicorn seals, Greek accounts" \
http://localhost:8080/api/load