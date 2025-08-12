# Projeto de Automação com Ansible para Docker Swarm

Este projeto utiliza o Ansible para automatizar por completo o provisionamento e a configuração de um cluster Docker Swarm, incluindo a implantação de uma aplicação de exemplo.

## O que o projeto faz?

O playbook principal (`playbook.yaml`) executa as seguintes ações:

1. **Instala Nginx**: Instala e inicia o Nginx em todos os nós do cluster (manager e workers).
2. **Configura o Cluster Swarm**:
    * Prepara os nós instalando dependências base e o Docker.
    * Inicializa o Docker Swarm no nó **manager**.
    * Adiciona os nós **workers** ao cluster.
3. **Implanta a Aplicação**: Faz o deploy de uma stack de serviços Docker (definida no role `deploy_stack`) no manager para ser executada no cluster.

## Pré-requisitos

Antes de executar, você precisa ter instalado na sua máquina local (o nó de controle Ansible):

* Python
* Ansible

As dependências Python do projeto podem ser instaladas com o pip:

```bash
pip install -r requirements.txt
```

## Configuração

1. **Inventário de Hosts**:
    Edite o arquivo `hosts` para refletir o seu ambiente. Substitua os endereços de IP de exemplo pelos IPs reais das suas máquinas `manager` and `workers`.

    ```ini
    [manager]
    ip_do_seu_manager

    [workers]
    ip_do_seu_worker_1
    ip_do_seu_worker_2
    ```

2. **Chave SSH**:
    No final do arquivo `hosts`, atualize o caminho para a sua chave SSH privada, que será usada para se conectar às máquinas.

    ```ini
    [all:vars]
    ansible_ssh_private_key_file=/caminho/para/sua/chave.pem
    ansible_user=ubuntu
    ```

    O usuário (`ansible_user`) também pode ser ajustado se necessário.

## Como Executar

Após a configuração do inventário, execute o playbook principal com o seguinte comando:

```bash
ansible-playbook playbook.yaml
```

O Ansible se conectará aos servidores, executará todas as tarefas de configuração e, ao final, sua aplicação estará rodando no cluster Docker Swarm.
