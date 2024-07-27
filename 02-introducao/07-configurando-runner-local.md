# Passo a passo para configuração do Runner localmente.

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
