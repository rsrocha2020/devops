A arquitetura envolvendo Kubernetes, Jenkins e Harbor. Pipelines CI/CD moderno, ambiente de sustentação em on-premises, abaixo uma visão geral da arquitetura e como os componentes interagem:


📐 Arquitetura: Kubernetes + Jenkins + Harbor

1. Componentes Principais
Kubernetes Cluster (K8s):

Orquestrador de contêineres.

Hospeda aplicações, microserviços e o próprio Jenkins se desejado.

Pode ser bare-metal ou em nuvem.


Jenkins (CI/CD):

Ferramenta de integração e entrega contínua.

Cria pipelines para build, test, push e deploy.

Pode rodar dentro do Kubernetes ou em uma VM separada.

Harbor (Registro de Imagens):

Registry privado de imagens Docker.

Garante segurança (scan de vulnerabilidades, controle de acesso).

Integra com o Jenkins (push) e Kubernetes (pull).


🔁 Fluxo de CI/CD

Dev → Git Push → Jenkins Pipeline → Build Imagem → Push p/ Harbor → Deploy no K8s
Desenvolvedor faz commit/push no repositório.

Jenkins é acionado por webhook.

Jenkins:

Faz o build da imagem Docker.

Faz o push da imagem para o Harbor.

Aplica um kubectl apply -f ou usa Helm para atualizar o deployment no Kubernetes.

Kubernetes baixa a imagem do Harbor e aplica o deployment.


🖥️ Visão de Infraestrutura

![image](https://github.com/user-attachments/assets/ff7216b6-3c49-4d4f-a321-c52de5cb8f59)


Kubernetes (01 Master node e 03 Worker node):

![image](https://github.com/user-attachments/assets/2cc7bfa6-f13e-47b5-813c-bef8a88b4e5a)

NGINX Ingress Controller:

![image](https://github.com/user-attachments/assets/e90a62b2-8737-45d5-a414-b6a00ea4e3f6)


Jenkins Server:

![image](https://github.com/user-attachments/assets/edb6f2bf-9294-4e31-a28d-10798c179b88)

Harbor:

![image](https://github.com/user-attachments/assets/efffd9bb-d5d2-4a5c-bab5-8a07d8a78b03)



Configurado Ingress Controller + TLS para acesso seguro as Apps, Jenkins e Harbor.

Utilizando PVCs para persistência no Jenkins e Harbor.

Scan de imagens no Harbor para segurança.
