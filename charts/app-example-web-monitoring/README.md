### Chart Helm de exemplo

O objetivo deste chart Helm é exemplificar o ciclo de vida de uma aplicação no Kubernetes com criação e remoção de monitoramento web no Zabbix.

Pré-requisitos para testar este chart:

- Acesso a API do Kubernetes
- Cliente helm instalado
- Usuário com permissão no Zabbix
- ID do host em que se deseja criar o cenário web

Para testar, siga os passos a seguir:

- Defina o arquivo de YAML com os parâmetros de ```values``` desejado.

$ vim /tmp/teste-zabbix.yaml
```yaml 
ingress:
  enabled: true
  hosts:
    - host: teste-app.whitelabel.com.br
      paths:
        - path: /
          pathType: ImplementationSpecific

webScenario:
  enabled: true
  zabbixUrl: "" # URL de API do Zabbix. Exemplo: https://zabbix.whitelabel.com.br/api_jsonrpc.php
  zabbixUser: "" # Usuário Zabbix
  zabbixPassword: "" # Senha do usuário Zabbix
  monitoringUrl: "" # URL de monitoramento desejada. Pode ser igual ao informado no Ingress.
  code: "200" # Código de retorno desejado 
  hostId: "" # Capture o ID do Host no Zabbix
```

- Para instalar, execute:

```shell
$ helm install -n app-teste --create-namespace ns-teste -f /tmp/teste-zabbix.yaml app-example-web-monitoring/
```

- Para remover, execute:

```shell
helm uninstall app-teste -n ns-teste
```
