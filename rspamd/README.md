# rspamd

Rspamd

![Version: 0.8.0](https://img.shields.io/badge/Version-0.8.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2.3.13-alpine3.13.2](https://img.shields.io/badge/AppVersion-2.3.13--alpine3.13.2-informational?style=flat-square)  [![rspamd](https://github.com/ectobit/charts/actions/workflows/rspamd.yml/badge.svg)](https://github.com/ectobit/charts/actions/workflows/rspamd.yml)

## Add repository

`helm repo add ectobit https://charts.ectobit.com`

## Install

```sh
helm install rspamd ectobit/rspamd
```

## Helmfile

```yaml
releases:
- name: rspamd
  chart: ectobit/rspamd
  - redis:
      enabled: true
      cluster:
        enabled: false
      serviceAccount:
        create: true
      rbac:
        create: true
      usePassword: false
      master:
        persistence:
          enabled: true
          size: 128Mi
  - persistence:
      enabled: true
      size: 4Mi
```

## Additional configuration (manual)

```sh
rspamadm configwizard
rspamadm dkim_keygen -b 2048 -s 2020 -k /var/lib/rspamd/dkim/2020.key > /var/lib/rspamd/dkim/2020.txt
```

Take care to use the same key name as in values config.dkimSelector.

## Alternative way to check health

```sh
curl -f -L http://localhost:11334/ || exit 1
```

## References

- [Mailserver mit Dovecot, Postfix, MySQL und Rspamd unter Debian 10 Buster](https://thomas-leister.de/mailserver-debian-buster/) by Thomas Leister

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | redis | 12.7.4 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| config.blacklist.fromMap | string | `""` |  |
| config.blacklist.ipMap | string | `""` |  |
| config.dkimSelector | int | `2020` |  |
| config.milterHeaders | string | `"use = [\"x-spamd-bar\", \"x-spam-level\", \"authentication-results\"];\nauthenticated_headers = [\"authentication-results\"];\n"` |  |
| config.multiMap | string | `"WHITELIST_IP {\n  type = \"ip\";\n  map = \"$CONFDIR/local.d/whitelist_ip.map\";\n  description = \"Local ip whitelist\";\n  action = \"accept\";\n}\n\nWHITELIST_FROM {\n  type = \"from\";\n  map = \"$CONFDIR/local.d/whitelist_from.map\";\n  description = \"Local from whitelist\";\n  action = \"accept\";\n}\n"` |  |
| config.overrideClassifierBayes | string | `"autolearn = true;\n"` |  |
| config.whitelist.fromMap | string | `""` |  |
| config.whitelist.ipMap | string | `""` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ectobit/rspamd"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| persistence.accessMode | string | `"ReadWriteOnce"` |  |
| persistence.annotations | object | `{}` |  |
| persistence.enabled | bool | `false` |  |
| persistence.size | string | `"128Mi"` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext.fsGroup | int | `101` |  |
| redis.enabled | bool | `false` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.controllerPort | int | `11334` |  |
| service.port | int | `11333` |  |
| service.proxyPort | int | `11332` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` |  |