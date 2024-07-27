# Explicando e configurando Runner Shell e instalando Runner Docker no [Gitlab.com](https://docs.gitlab.com/).

## Oque é o Gitlab Runner?

O GitLab Runner é um aplicativo que funciona com o GitLab CI/CD para executar trabalhos em um pipeline. Você pode optar por instalar o aplicativo GitLab Runner na infraestrutura que voce possui ou gerencia. Se fizer isso, instale o Gitlab Runner em um maquina separada daquela que hospeda a instancia do Gitlab por motivos de segurança e desempenho. Ao usar maquinas separadas, voce pode ter diferentes sistemas operacionais e ferramenas, como kubernetes ou Docker, em cada uma.

### Tipos de Runner:

- [Linux](https://docs.gitlab.com/runner/install/linux-repository.html). 

- [macOS](https://docs.gitlab.com/runner/install/osx.html). 

- [Windows](https://docs.gitlab.com/runner/install/windows.html).

## Para que serve o Runner?

Basicamente o Runner é o local onde executamos os comandos / scripts que são chamados no arquivo `gitlab-ci.yaml`.

## Passo a passo para configuração do Runner no `GITLAB.COM`.

- [ ] 1️⃣ Ingressar o Runner em modo shell no Gitlab

```bash
sudo gitlab-runner register -n \
  --url http://IP-OU-URL \
  --registration-token TOKEN \
  --executor shell \
  --description "Runner Shell"
```

- [ ] 2️⃣ - Criar o container gitlab-runner para o Docker
> **OBS:** Se estiver utilizando gitlab.com ou certificado, altere para HTTPS://

```bash
docker run -dit \
  --name runner-docker \
  --restart always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /opt/gitlab-runner/config:/etc/gitlab-runner \
  gitlab/gitlab-runner:ubuntu-v14.9.1
```

- [ ] 3️⃣ - Ingressar o Runner em modo docker no GitLab.
> **OBS:** Se estiver utilizando gitlab.com ou certificado, altere para HTTPS://

```bash
docker exec -it runner-docker \
gitlab-runner register -n \
  --url http://IP-OU-URL \
  --registration-token TOKEN \
  --clone-url http://IP-OU-URL\
  --executor docker \
  --docker-image "docker:latest" \
  --docker-privileged
```