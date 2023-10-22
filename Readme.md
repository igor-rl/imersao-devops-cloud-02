# Imersão DevOps && Cloud 

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