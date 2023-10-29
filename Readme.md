# Imersão DevOps & Cloud com Fabrício Venonez

Este repositório contém todo o trabalho e aprendizado que adquiri no curso de DevOps & Cloud com Fabrício Venonez.

## Sobre o Projeto: Kube-news

Kube-news é um blog de notícias que foi implantado utilizando várias ferramentas e plataformas durante o curso:

- **Docker**: Usado para contêinerizar a aplicação.
- **k3D com Kubernetes**: Permite orquestrar os contêineres da aplicação.
- **AWS**: Plataforma de computação em nuvem onde a aplicação foi implantada.

## CI/CD & Infraestrutura como Código

- **Git Actions**: Utilizado para criar um pipeline de Integração Contínua e Entrega Contínua (CI/CD), garantindo que a aplicação seja construída, testada e implantada de forma automática.
- **Terraform**: Ferramenta escolhida para criar e gerenciar a infraestrutura na AWS de forma automatizada e reproduzível.

## Como usar

1. Clone o repositório:
```bash
git clone https://github.com/igor-rl/imersao-devops-cloud-02.git
```


2. Navegue até o diretório:
```bash
cd imersao-devops-cloud-02
```

3. Siga as instruções específicas no arquivo `INSTALL.md` para configurar e implantar a aplicação.

## Kubernetes

Comando para criar o cluster com k3d e executar a aplicação:
```Bash
k3d cluster create meucluster -p "8080:30000@loadbalancer"
```

Modifique o type do service para:
```yml
type: NodePort
```

Crie os clusters:
```yml
kubectl apply -f kube-news/k8s/
```

Acesse o app em [http://localhost:8080](http://localhost:8080).


Encerrar:
```yml
kubectl delete -f kube-news/k8s/
```

## Terraform

Configurar a cli da aws:
```yml
aws configure
```

Gerar os arquivos e dependencias terraform:
```yml
terraform init
```

Gerar o plano de modificações:
```yml
terraform plan
```

Aplicar as modificações:
```yml
terraform apply
```

digite yes para confirmar as modificações

```yml
aws eks update-kubeconfig --name imersao-eks
```

Aguarde o cluster ser criado e estar pronto. Depois basta aplicar seu deploy:
```yml
kubectl apply -f kube-news/k8s/
```

Após isso, para acessar o app use o comando:
```yml
explorer.exe "http://$(kubectl get svc kubenews -o=jsonpath='{.status.loadBalancer.ingress[0].hostname}')"
```

Encerrar o projeto:
```yml
kubectl delete -f kube-news/k8s/
```
```yml
terraform destroy
```

digite 'yes'

## Contribuições

Contribuições são sempre bem-vindas! Sinta-se à vontade para abrir uma issue ou enviar um pull request.

## Licença

Este projeto está sob a licença MIT. Consulte o arquivo `LICENSE.md` para obter detalhes.

## Agradecimentos

Um agradecimento especial a Fabrício Venonez por compartilhar seu conhecimento e experiência no mundo DevOps e Cloud!
