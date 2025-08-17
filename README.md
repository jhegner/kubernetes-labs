![K8s Labs Path](images/k8s_lab_path.png)

## Laboratório para aprendizado e teste da plataforma _Kubernetes_

Bem-vindo ao repositório `kubernetes-labs`!

Com este laboratório desejamos aprender mais sobre:

1. Arquitetura 
2. Kubernetes
3. CI/CD (devops)
4. Observability
5. Security

### Links importantes

- https://kubernetes.io/
- https://landscape.cncf.io/
- https://www.vultr.com/
- https://argoproj.github.io/
- https://grafana.com/
- https://github.com/features/actions
- https://semver.org/
- https://nvie.com/posts/a-successful-git-branching-model/
- https://developer.hashicorp.com/terraform
- https://www.conventionalcommits.org/pt-br/v1.0.0/
- https://mockapi.io/

### Ferramentas e serviços

- https://registro.br/

### Articles
- https://github.com/resources/articles/devops/ci-cd

### Documentação
- [Kubernetes](/docs/kubernetes/README.md)
- [Pipeline](/docs/pipeline/README.md)
- [Repos](/docs/repos/README.md)


### Projetos do Lab
- [infra-demo](https://github.com/jhegner/kubernetes-labs-infra-demo)
- [app-micronout](https://github.com/jhegner/kubernetes-labs-app-micronout)
- [ci-workflows](https://github.com/jhegner/kubernetes-labs-ci-workflows)
- [infra-cloud-vultr](https://github.com/jhegner/kubernetes-labs-infra-cloud-vultr)
- [infra-vkecluster](https://github.com/jhegner/kubernetes-labs-infra-vkecluster)

### Segredos e variáveis de ambiente
> Para execução das pipelines de infra e apps é necessário cadastrar os seguintes segredos ou variáveis de ambiente em cada repositório com respectivos valores em:
Settings > Security > Secrets and variables > Actions
- GH_TOKEN
- SONAR_TOKEN						
- SONAR_KEY						
- VULTR_API_KEY					
- VULTR_REGISTRY_URN				
- VULTR_REGISTRY_USERNAME			
- VULTR_REGISTRY_PASSWORD			
- VULTR_CONTAINER_REGISTRY_NAME	
- AWS_ACCESS_KEY_ID				
- AWS_SECRET_ACCESS_KEY			
- MOCKAPI_PROJECT_SECRET

