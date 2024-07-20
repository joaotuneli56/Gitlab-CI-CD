# Instalando Gitlab e Docker localmente

Nesse capitulo utilizaremos os scripts `04-install-gitlab.sh`, para instalar o ususario root do gitlab em nossa maquina local

**Documentação ofical do [GitLab]( https://docs.gitlab.com/ee/install/docker.html) para instalação.**

## Explicação do script `04-install-gitlab.sh` e algumas configurações antes da instalação.

Explicando a fundo o que o script faz, segue o script por completo e abaixo algumas explicações do que estamos configurando.

```bash
#!/bin/bash

sudo mkdir -p /storage/docker-homol/deploy/gitlab/{data,logs,config}

docker run -dit \
  -p "2222:22" \
  -p "80:80" \
  -p "443:443" \
  --name gitlab \
  --hostname IP-DO-SERVER \
  -v /storage/docker-homol/deploy/gitlab/data:/var/opt/gitlab \
  -v /storage/docker-homol/deploy/gitlab/logs:/var/log/gitlab \
  -v /storage/docker-homol/deploy/gitlab/config:/etc/gitlab \
  --shm-size 256m \
  gitlab/gitlab-ce:14.7.6-ce.0

# REFERENCIA: https://docs.gitlab.com/ee/install/docker.html
``` 
### 1️⃣ Comando 
- [ ] Nesse script, primeriamente criamos alguns diretorios para persistir os dados do gitlab, como logs, configurações e dados sensiveis.

```bash
sudo mkdir -p /storage/docker-homol/deploy/gitlab/{data,logs,config}
```

### 2️⃣ Comando
- [ ] Depois executamos a criação do container do GitLab.

```bash
ocker run -dit \
  -p "2222:22" \
  -p "80:80" \
  -p "443:443" \
  --name gitlab \
  --hostname IP-DO-SERVER \
  -v /storage/docker-homol/deploy/gitlab/data:/var/opt/gitlab \
  -v /storage/docker-homol/deploy/gitlab/logs:/var/log/gitlab \
  -v /storage/docker-homol/deploy/gitlab/config:/etc/gitlab \
  --shm-size 256m \
  gitlab/gitlab-ce:14.7.6-ce.0
```

> **OBS:** Caso vc não consigo executar o comando `docker ps -a`, será necessario inserir seu ususario no grupo docker:

```bash
sudo usermod -aG docker <nome_do_seu_usuario_root>
# Será necesssario reiniciar o Sistema Operacional

```

## Passo a Passo para a instalação.

- [ ] 1️⃣ - Rodar o script para a criação das pastas e do conteiner do gitlab.

```bash
# 1° Entrar na pasta onde estão os scripts
cd 02-introducao/resources

# 2º ROdar o script
./ 04-install-gitlab.sh
```

- [ ] 2️⃣ - Pegar a senha do primeiro acesso do gitlab
```bash
sudo docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```

- [ ] 3️⃣ - Pegar o ip da sua maquina.
```bash
hostname -I
```

- [ ] 4️⃣ - Utilizando a porta 80, digite seu ip no seu browser:
```
http://192.168.0.204:80
```

- [ ] 5️⃣ - Faça o acesso com a senha temporaria utilizando a palavra `root` na campo usuário.

- [ ] 6️⃣ - Pra finalizar altere a senha temporaria
