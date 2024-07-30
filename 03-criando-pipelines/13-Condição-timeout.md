# Condição de Timeout

O timeout padrão dos jobs é de 1 hora, então utilizando o timeout conseguimos alterar essa janela de horario padrão.

Então por exemplo:

```yaml
job3:
  timeout: 1m
  script:
    - sleep 20
    - echo "Executa com timeout de 1 minuto" 
```

Nesse yaml alteramos o timeout da pipeline de 1 hora para 1 minuto. Agora para forçar o timeout , podemos coloar um tempo de expiração de 20 segundos e pedir para a pipeline executar um sleep de 25 segundos:

```yaml
job3:
  timeout: 20s
  script:
    - sleep 25
    - echo "Executa com timeout de 1 minuto" 
```

#### Documentação oficial --> [Documentação Timeout](https://docs.gitlab.com/ee/ci/yaml/#timeout)