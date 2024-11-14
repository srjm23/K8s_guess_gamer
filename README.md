# Kubernetes Deployment with Minikube

Este repositório contém os manifestos para implantação de um banco de dados, backend e frontend utilizando Minikube e Kubernetes. Siga os passos abaixo para executar os comandos necessários para configurar e rodar os serviços.

## Requisitos

- [Minikube](https://minikube.sigs.k8s.io/docs/) instalado
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) configurado para usar o Minikube
- Manifests YAML para os recursos Kubernetes

## Passos para execução

1. **Iniciar o Minikube**

Caso o Minikube não esteja em execução, inicie-o com o seguinte comando:

```bash
minikube start
```
2. **Aplicar o SecretDB.yaml**

```bash
kubectl apply -f SecretDB.yaml
```
Este comando aplica o arquivo SecretDB.yaml, que contém as credenciais de acesso ao banco de dados em formato de Secret. O Kubernetes armazena esses dados de maneira segura, permitindo que sejam referenciados por outros recursos de forma protegida.

3. **Aplicar o PersistenteVolumeDB.yaml**
```bash
kubectl apply -f PersistenteVolumeDB.yaml
```
Este comando aplica a configuração de um volume persistente para armazenar os dados do banco de dados. O arquivo PersistenteVolumeDB.yaml define as especificações do volume, garantindo que os dados do banco de dados sejam preservados mesmo após reinicializações de pods.

4. **Aplicar o DeploymentDB.yaml**
```bash
kubectl apply -f DeploymentDB.yaml
```
O comando aplica o DeploymentDB.yaml, que cria o Deployment do banco de dados. O Deployment define quantas réplicas do banco de dados serão executadas e como o contêiner do banco de dados deve ser configurado.

5. **Aplicar o ServiceDB.yaml**
```bash
kubectl apply -f ServiceDB.yaml
```
Este comando aplica o arquivo ServiceDB.yaml, criando um Service para o banco de dados. O Service permite que outros recursos, como o backend da aplicação, se comuniquem com o banco de dados.

6. **Aplicar o DeploymentBack.yaml**
```bash
kubectl apply -f DeploymentBack.yaml
```
Este comando aplica o DeploymentBack.yaml, que cria o Deployment para a camada de backend da aplicação. Ele define as especificações do contêiner backend, incluindo o número de réplicas e outras configurações.

7. **Aplicar o ServiceBackend.yaml**
```bash
kubectl apply -f ServiceBackend.yaml
```
O comando aplica o ServiceBackend.yaml, que cria um Service para o backend da aplicação. Este Service expõe o backend para comunicação com outros serviços, como o frontend.

8. **Aplicar o HpaBackend.yaml**
```bash
kubectl apply -f HpaBackend.yaml
```
Este comando aplica o arquivo HpaBackend.yaml, que define uma Auto-Scaling Policy (Horizontal Pod Autoscaler) para o backend. O HPA ajusta o número de réplicas do backend com base na carga de trabalho, como o uso de CPU.

9. **Aplicar o DeploymentFront.yaml**
```bash
kubectl apply -f DeploymentFront.yaml
```
O comando aplica o DeploymentFront.yaml, que cria o Deployment para o frontend da aplicação. Este Deployment define as configurações do contêiner do frontend, incluindo o número de réplicas.

10. **Aplicar o ServiceFrontend.yaml**
```bash
kubectl apply -f ServiceFrontend.yaml
```
Este comando aplica o ServiceFrontend.yaml, criando um Service para o frontend. O Service permite que o frontend se comunique com o backend e seja acessado pelos usuários.

11. **Redirecionamento de Porta para o Frontend**
```bash
kubectl port-forward service/frontend 3000:80
```
Este comando realiza o redirecionamento de porta, permitindo que o serviço do frontend seja acessado localmente na porta 3000. O comando mapeia a porta 80 do serviço frontend para a porta 3000 na sua máquina local.