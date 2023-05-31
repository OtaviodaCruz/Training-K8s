# Training-K8s

Conceitos basicos de K8s:

- Deploymente (implantação)
- Scaling (horizontal e vertical)

K8s utiliza arquivos de configuração YAML. 

## Contém 

Por enquanto está sendo utilizado containers ubuntu como forma de exemplificar os conceitos

- ubuntu_deploy.yaml: implementa o conceito de Deploymente com replicas.
- ubuntu_deploy.yaml + ubuntu_with_scaling.yaml: implementa o conceito de scaling baseado em consumo de CPU (deprecated).
- php-apache.yaml + scaling-apache.yaml: teste com auto scaling baseado em consumo de CPU.


## Uso

- Instale K3s versão v1.26.4 (8d0255af).

### Deployment

- Aplique:

```kubectl apply -f ubuntu_deploy.yaml```

- Para verificar a implantação:

```kubectl get pods```

### Auto scaling horizontal (HPA)

- Aplica deploymet de uma aplicação apache

```kubectl apply -f php-apache.yaml```

- Aplica scaling baseado em uso de CPU

```kubectl apply -f scaling-apache.yaml```

Obs.: Também e possivel utilizar o comando ```kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10```

- Verifique o hpa aplicado
  
```kubectl get hpa```

- Simule um aumento de carga

```kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"```

- Assista o aumento de replicas conforme o aumendo de consumo de CPU

```kubectl get hpa php-apache --watch```

Referência: [kubernetes.io](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/)



