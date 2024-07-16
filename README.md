# Sistema de Integração de Dados com Airflow, Postgres e Redis

## Visão Geral

Este projeto configura um sistema de integração de dados utilizando Apache Airflow, Postgres e Redis. O Docker Compose é usado para orquestrar os serviços necessários para executar o Airflow em um ambiente distribuído, garantindo alta disponibilidade e escalabilidade.

## Componentes Principais

1. **Postgres**: Banco de dados para armazenamento de metadados do Airflow.
2. **Redis**: Broker de mensagens para a fila de tarefas do Celery Executor.
3. **Airflow Webserver**: Interface web para monitorar e gerenciar os DAGs.
4. **Airflow Scheduler**: Agendador de tarefas do Airflow.
5. **Airflow Worker**: Trabalha na execução das tarefas do Airflow.
6. **Airflow Triggerer**: Componente responsável por disparar tarefas baseadas em eventos.
7. **Airflow Init**: Serviço inicializador para configurar o ambiente Airflow.
8. **Airflow CLI**: Interface de linha de comando do Airflow.
9. **Flower**: Interface web para monitoramento do Celery.

## Estrutura do Projeto

### Serviços e Configurações

- **Postgres**:
  - Imagem: `postgres:13`
  - Porta: `5432`
  - Variáveis de ambiente: `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`
  - Volume: `postgres-db-volume`
  - Healthcheck: Verifica se o banco de dados está pronto

- **Redis**:
  - Imagem: `redis:latest`
  - Porta: `6379`
  - Healthcheck: Verifica se o Redis está respondendo

- **Airflow**:
  - Imagem: `apache/airflow:2.5.1`
  - Volumes: Monta diretórios locais para DAGs, logs e plugins
  - Environment: Configurações do Airflow, incluindo conexões de banco de dados e broker
  - Healthchecks: Verificações de saúde específicas para cada serviço do Airflow

## Como Executar

### Pré-requisitos

- Docker
- Docker Compose

### Passos para Iniciar

1. Clone o repositório:
    ```sh
    git clone https://github.com/seu-usuario/seu-repositorio.git
    cd seu-repositorio
    ```

2. Inicie os serviços:
    ```sh
    docker-compose up -d
    ```

3. Acesse a interface web do Airflow:
    - URL: [http://localhost:8080](http://localhost:8080)
    - Usuário: `airflow`
    - Senha: `airflow`

4. Monitore o Celery com o Flower:
    - URL: [http://localhost:5555](http://localhost:5555)

## Estrutura de Diretórios

- **dags/**: Contém os DAGs (scripts de fluxo de trabalho) do Airflow.
- **logs/**: Diretório onde os logs de execução dos DAGs são armazenados.
- **plugins/**: Diretório para plugins customizados do Airflow.

## Dependências

- **Volumes**:
  - `postgres-db-volume`: Armazena dados persistentes do Postgres

## Considerações Finais

Este setup proporciona um ambiente robusto e escalável para gerenciar e monitorar fluxos de trabalho com o Airflow. As configurações podem ser ajustadas conforme necessário para atender requisitos específicos de projeto ou ambiente.

Para mais informações, consulte a [documentação do Airflow](https://airflow.apache.org/docs/).