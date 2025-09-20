# AWS SOLUTION ARCHITETURES
<details>
<summary>🇺🇸 View in English</summary>

## Serverless Architecture for Image Processing on AWS

This repository contains the documentation of a serverless system architecture, built on AWS, designed to receive image uploads, process them (resizing), and notify the user upon completion.

### Architecture Diagram

The diagram below illustrates the data flow and the components involved in the solution.

### How It Works

The system's operational flow occurs in 5 main steps, in a fully managed and event-driven manner:

**User Request:** The user starts the process by sending an image via an HTTP request to an API endpoint.

**API Gateway:** The API Gateway acts as the entry point, receiving the HTTP request. It is responsible for validating the call and securely forwarding it to the processing function.

**AWS Lambda:** The Lambda function is the brain of the operation. It is triggered by the API Gateway and executes the main business logic: it receives the image, resizes it to a standard size, and prepares it for storage.

**Amazon S3:** After processing, the Lambda function saves the new resized image to an Amazon S3 bucket, which serves as a durable and highly available object repository.

**Amazon SNS (Notification):** The S3 bucket is configured to trigger an event whenever a new object is created. This event publishes a message to an Amazon SNS topic, which in turn notifies the user (via email, SMS, or another service) that their image upload and processing have been successfully completed.

### Components Used

* **API Gateway:** A managed service that acts as a front door for the application, exposing an HTTP endpoint to the external world.
* **AWS Lambda:** A serverless compute service that executes the image resizing code without the need to manage servers.
* **Amazon S3 (Simple Storage Service):** An object storage service used to store the processed images securely and scalably.
* **Amazon SNS (Simple Notification Service):** A messaging (Pub/Sub) service used to decouple the system and manage the sending of notifications after processing.

---

## Dedicated Game Server Architecture on AWS

This repository documents a classic server architecture on AWS, using an EC2 instance with a persistent EBS volume. This model, based on the IaaS (Infrastructure as a Service) pattern, is the foundation for hosting a wide range of applications, such as dedicated game servers, dynamic websites, or systems that require a traditional server environment.

### Architecture Diagram

The diagram below illustrates the interaction between the users, the application server, and its persistent storage.

### How It Works

The flow of this architecture is direct and robust, centered on the compute instance and its attached storage.

**User Connection:** The players (users) connect directly to the server over the internet, using the public IP address of the EC2 instance.

**Processing on EC2:** The Amazon EC2 instance acts as the brain and computing power (CPU, RAM) of the operation. It is responsible for running the game server software, processing the game logic in real-time, and managing player connections.

**Persistent Storage on EBS:** Directly attached to the EC2 instance, the Amazon EBS volume functions as the server's primary and persistent hard drive (HD). The EC2 instance constantly reads and writes data to this volume.

**Data Stored:** The EBS volume is crucial for data persistence, ensuring that no information is lost if the server is restarted. It stores all essential components:

* The **Operating System** (e.g., Linux or Windows).
* The **game server** application files.
* A **Database** (running on the EC2) that stores vital information such as player accounts, logs, inventories, and game progress.

### Components Used

* **Amazon EC2 (Elastic Compute Cloud):** The compute service that provides the processing capacity (the virtual server) to run the game application. It is the heart of the infrastructure.
* **Amazon EBS (Elastic Block Store):** Provides the persistent block storage volume (the "HD") for the EC2 instance. Its main function is to ensure that the data for the operating system, application, and database persist regardless of the EC2 instance's lifecycle.

</details>

# Arquitetura Serverless para Processamento de Imagens na AWS

Este repositório contém a documentação de uma arquitetura de sistema serverless, construída na AWS, projetada para receber o upload de imagens, processá-las (redimensionar) e notificar o usuário sobre a conclusão.

## Diagrama da Arquitetura

O diagrama abaixo ilustra o fluxo de dados e os componentes envolvidos na solução.

![Diagrama da Arquitetura Serverless](https://github.com/marianachoratto/aws-solution-architectures/blob/main/Diagrama%201-%20S3.drawio.svg)

---

## Como Funciona

O fluxo de operação do sistema ocorre em 5 passos principais, de forma totalmente gerenciada e orientada a eventos:

1.  **Requisição do Usuário:** O usuário inicia o processo enviando uma imagem através de uma requisição HTTP para um endpoint de API.

2.  **API Gateway:** O **API Gateway** atua como a porta de entrada, recebendo a requisição HTTP. Ele é responsável por validar a chamada e encaminhá-la de forma segura para a função de processamento.

3.  **AWS Lambda:** A função **Lambda** é o cérebro da operação. Ela é acionada pelo API Gateway e executa a lógica de negócio principal: recebe a imagem, a redimensiona para um tamanho padrão e a prepara para armazenamento.

4.  **Amazon S3:** Após o processamento, a função Lambda salva a nova imagem redimensionada em um bucket do **Amazon S3**, que serve como um repositório de objetos durável e altamente disponível.

5.  **Amazon SNS (Notificação):** O bucket S3 é configurado para disparar um evento sempre que um novo objeto é criado. Esse evento publica uma mensagem em um tópico do **Amazon SNS**, que por sua vez notifica o usuário (via e-mail, SMS, ou outro serviço) que o upload e o processamento da sua imagem foram concluídos com sucesso.

---

## Componentes Utilizados

* **API Gateway:** Serviço gerenciado que atua como uma porta de segurança para a aplicação, expondo um endpoint HTTP para o mundo externo.
* **AWS Lambda:** Serviço de computação serverless que executa o código de redimensionamento da imagem sem a necessidade de gerenciar servidores.
* **Amazon S3 (Simple Storage Service):** Serviço de armazenamento de objetos utilizado para guardar as imagens processadas de forma segura e escalável.
* **Amazon SNS (Simple Notification Service):** Serviço de mensageria (Pub/Sub) usado para desacoplar o sistema e gerenciar o envio de notificações após o processamento.


# Arquitetura de Servidor de Jogo Dedicado na AWS

Este repositório documenta uma arquitetura clássica de servidor na AWS, utilizando uma instância EC2 com um volume EBS persistente. Este modelo, baseado no padrão IaaS (Infrastructure as a Service), é a fundação para hospedar uma vasta gama de aplicações, como servidores de jogos dedicados, sites dinâmicos ou sistemas que necessitam de um ambiente de servidor tradicional.

## Diagrama da Arquitetura

O diagrama abaixo ilustra a interação entre os usuários, o servidor de aplicação e seu armazenamento persistente.

![Diagrama da Arquitetura do Servidor de Jogo](https://github.com/marianachoratto/aws-solution-architectures/blob/main/Diagrama%20sem%20nome.drawio.png)

---

## Como Funciona

O fluxo desta arquitetura é direto e robusto, centrado na instância de computação e seu armazenamento atachado.

1.  **Conexão dos Usuários:** Os jogadores (usuários) se conectam diretamente ao servidor através da internet, utilizando o endereço de IP público da instância EC2.

2.  **Processamento na EC2:** A instância **Amazon EC2** atua como o cérebro e a força de computação (CPU, RAM) da operação. Ela é responsável por executar o software do servidor de jogo, processar a lógica do jogo em tempo real e gerenciar as conexões dos jogadores.

3.  **Armazenamento Persistente no EBS:** Diretamente atachado à instância EC2, o volume **Amazon EBS** funciona como o disco rígido (HD) principal e persistente do servidor. A EC2 lê e escreve dados neste volume constantemente.

4.  **Dados Armazenados:** O volume EBS é crucial para a persistência dos dados, garantindo que nenhuma informação seja perdida caso o servidor seja reiniciado. Ele armazena todos os componentes essenciais:
    * O **Sistema Operacional** (ex: Linux ou Windows).
    * Os arquivos da aplicação do **servidor de jogo**.
    * Um **Banco de Dados** (rodando na EC2) que guarda informações vitais como contas de jogadores, logs, inventários e progresso no jogo.

---

## Componentes Utilizados

* **Amazon EC2 (Elastic Compute Cloud):** É o serviço de computação que fornece a capacidade de processamento (o servidor virtual) para executar a aplicação do jogo. É o coração da infraestrutura.
* **Amazon EBS (Elastic Block Store):** Fornece o volume de armazenamento em bloco persistente (o "HD") para a instância EC2. Sua principal função é garantir que os dados do sistema operacional, da aplicação e do banco de dados persistam independentemente do ciclo de vida da instância EC2.




