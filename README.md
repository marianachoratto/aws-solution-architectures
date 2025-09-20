# modelos-de-arquitetura-aws


# Arquitetura Serverless para Processamento de Imagens na AWS

Este repositório contém a documentação de uma arquitetura de sistema serverless, construída na AWS, projetada para receber o upload de imagens, processá-las (redimensionar) e notificar o usuário sobre a conclusão.

## Diagrama da Arquitetura

O diagrama abaixo ilustra o fluxo de dados e os componentes envolvidos na solução.

![Diagrama da Arquitetura Serverless](images/arquitetura-serverless.png)

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
