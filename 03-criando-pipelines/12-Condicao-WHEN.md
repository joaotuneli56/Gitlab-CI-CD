# Condição `When`

Utilizamos `when` para configurar as condições de execução dos trabalhos . Senão estiver definido em um trabalho, o valor padrão será igual `when: on_sucess`.

### Entradas possíveis

- `on_sucess`(default) - execute a tarefa somente quando todas as tarefas em estagios anteriores forem bem-sucedidas ou tiverem `allow_failure: true`.

- `manual` - Execute o trabalho somente quando acionado manualmente.

- `always` - execute o trabalho independentemente do status dos trabalhos nos estagios anteriores.

- `on_failure` - execute o trabalho somente quando pelo menos um trabalho em um estágio anterior falhar.

- `delayed` - Atrasar a execução de um trabalho por uma duração especifica.

- `never` - não execute o trabalho.

Segue alguns exemplos de pipelines utilizando o `when`.

### Exemplo 1
**Descrição** Nessa pipeline utilizamos o atributo **delayed**, que tem a função de iniciar um job apartir de um determinado tempo especulado no atributo `start_in`.

```yaml
job:
  when: delayed
  start_in: 1 minute
  script: echo "Execução em 1 minuto"
```

### Exemplo 2
**Descrição** Nessa pipe configuramos duas etapas, especificando as duas no atributo stage, e configurando o stage1(Etapa1) para rodar de qualquer jeito com o `on_sucess`, e o etage2(Etapa2), só irá rodar se a etapa 1 falhar.

```yaml
stages:
 - etapa1 
 - Etapa2

Etapa1:
  stage: etapa1
  when: on_success
  script:
    - echo "etapa 1"

Etapa2:
  stage: etapa2
  when: on_failure
  script:
    - echo "etapa 2"
```
### Exemplo 3
**Descrição** Nessa pipeline adicionamos, uma etapa 3 que vai ser executada independente dos outros stages, com o atributo always

```yaml
stages:
 - etapa1 
 - Etapa2
 - etapa3

Etapa1:
  stage: etapa1
  when: on_success
  script:
    - echo "etapa 1"

Etapa2:
  stage: etapa2
  when: on_failure
  script:
    - echo "etapa 2"

Etapa3:
  stage: etapa2
  when: always
  script:
    - echo "sempre será executado"
```

#### Documentação oficial --> [when](https://docs.gitlab.com/ee/ci/yaml/#when)