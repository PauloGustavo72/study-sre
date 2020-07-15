# Comando para subir o kafka, grafana e prometheus

## Para subir os projetos basta executar o comando abaixo:
   ``` sh
   docker-compose up -d 
   ```
    
    
## Explicando a coisa ..
    
   * Adicionamos o arquivo de [configuração](https://github.com/PauloGustavo72/study-sre/blob/master/monitoring/kafka/prom-jmx-agent-config.yml) e agente do prometheus na imagem do kafka:
   
   ```dockerfile
    ADD prom-jmx-agent-config.yml /usr/app/prom-jmx-agent-config.yml
    ADD https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.10/jmx_prometheus_javaagent-0.10.jar /usr/app/jmx_prometheus_javaagent.jar
   ```

   * Após isso, adicionamos a variável de configuração do kafka no docker-compose.yml, para que ele consiga usar o prometheus como um agente java e também desfrutar das [configurações](https://github.com/PauloGustavo72/study-sre/blob/master/monitoring/kafka/prom-jmx-agent-config.yml) criadas por nós: 

   ```dockerfile
    KAFKA_OPTS: -javaagent:/usr/app/jmx_prometheus_javaagent.jar=7071:/usr/app/prom-jmx-agent-config.yml
   ```

   * Próximo passo é executar o comando de construção do docker-compose.yml:
   ```shell script
    docker-compose up -d 
   ```
    
   * Depois de tudo inicializado temos duas opções:
        * Visualizar as métricas através do [Prometheus](http://localhost:9090/);
        * Visualizar as métricas através do [Grafana](http://localhost:3000/) adicionando o *Prometheus* com database e importando alguns [dashboards](). 



    

    