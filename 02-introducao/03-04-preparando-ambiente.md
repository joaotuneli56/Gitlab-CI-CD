# Preparando o ambiente Local e Web

Nesse curso foi apresentado duas maneiras de preparação de ambiente:

### 1º Gitlab online

- [ ] 1º paso criar sua conta na plataforma [gitlab](https://gitlab.com/dashboard/projects).

- [ ] 2º Valide sua conta.

- [ ] 3º Crie um grupo

- [ ] 4º para finalizar edite e configura seu perfil em preferencias.

### 2º Gitlab local

- [ ] 1º instalar o git.
```sudo apt git
```

- [ ] 2º clonar o seguinte [repositorio](https://gitlab.com/treinamentos1/pipeline/-/tree/main/install).
```
git clone https://gitlab.com/treinamentos1/pipeline.git
``` 

- [ ] 3º entre no diretorio do projeto, e depois dentro do diretorio e install.
```
cd pipeline
cd install
``` 
- [ ] 4º rode os scripts de instalação na seguinte ordem:
```
./01-install-docker.sh
./02-install-compose.sh
# Indico rodar o install do agente com sudo su
./03-install-agente.sh
./04-install-gitlab.sh
./05-config-runners.sh
```
