# Training-K8s

Conceitos basicos de K8s:

- Deploymente (implantação)
- Scaling (horizontal e vertical)

K8s utiliza arquivos de configuração YAML. 

## Contém 

Por enquanto está sendo utilizado containers ubuntu como forma de exemplificar os conceitos

- ubuntu_deploy.yaml: implementa o conceito de Deploymente com replicas.
- ubuntu_with_scaling.yaml: implementa o conceito de scaling a partir do consumo de CPU.

## Uso

- Instale K3s versão v1.26.4 (8d0255af).

- Aplique:

```kubectl apply -f <NOME DO ARQUIVO>```

- Para verificar a implantação:

```kubectl get pods```

- Para verificar o scaling horizontal:

```kubectl get hpa```
