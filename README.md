# Jenkins com Docker e Traefik

## Introdução
Jenkins é uma ferramenta de automação open-source usada para integração contínua (CI) e entrega contínua (CD). Ele permite a automação de diversas tarefas, como builds, testes e deploys de aplicações.

Este repositório contém um arquivo `docker-compose.yml` para executar o Jenkins em um ambiente Docker, integrando-o ao Traefik para gerenciamento de proxy reverso e certificados SSL automaticamente.

## Requisitos
Antes de iniciar, certifique-se de que seu ambiente atenda aos seguintes requisitos:

- Docker e Docker Compose instalados
- Traefik configurado e rodando na rede `traefik-net`
- Domínio configurado corretamente para acesso ao Jenkins

## Instalação
1. Clone este repositório:
   ```sh
   git clone https://github.com/jairisonsouza/jenkins.git
   cd jenkins
   ```

2. Certifique-se de que a rede `jenkins-net` existe, ou crie-a:
   ```sh
   docker network create --driver overlay --attachable jenkins-net
   ```

3. Execute o Jenkins com Docker Stack:
   ```sh
   docker stack deploy -c docker-compose.yml jenkins
   ```

4. Acesse o Jenkins no navegador:
   ```
   https://seudominio.com.br
   ```

5. Para acessar a senha inicial do Jenkins:
   ```sh
   docker exec -it <ID_DO_CONTAINER> cat /var/jenkins_home/secrets/initialAdminPassword
   ```

Substitua `<ID_DO_CONTAINER>` pelo ID do container em execução, que pode ser obtido com:
   ```sh
   docker ps
   ```

## Personalização
- Caso precise modificar a URL de acesso, altere a regra no Traefik dentro do `docker-compose.yml`.
- O assistente de configuração inicial do Jenkins está ativado pelo parâmetro `JAVA_OPTS`.

## Parar e Remover
Para parar e remover os serviços, use:
```sh
docker stack rm jenkins
```

Isso removerá os serviços, mas os dados do Jenkins permanecerão no volume `jenkins_home`.

## Contribuição
Sinta-se à vontade para contribuir com melhorias enviando pull requests ou relatando problemas!

## Licença
Este projeto é distribuído sob a licença MIT.
