---
name: OTA Update Issue
about: Reporte problemas específicos de atualização Over-The-Air (OTA)
title: "[OTA] "
labels: ["ota", "update"]
assignees: ""

---

## Descrição do Problema de Atualização

Descreva qual é o problema com a atualização OTA.

## Versão Atual do App

- Versão instalada: 
- Build Number: 

## Versão Esperada

- Versão no manifesto (`latestVersion`): 
- Build Number esperado: 

## Evidências de Diagnóstico

### Saída do `jq . app_update.json`:
```
Cole aqui a saída
```

### Código HTTP do `curl -sI` na URL do APK:
```
Cole aqui o código HTTP
```

### Valor do `sha256sum ArenaMatch-release.apk`:
```
Cole aqui o valor
```

### Resultado do `unzip -t ArenaMatch-release.apk`:
```
Cole aqui o resultado
```

## Dispositivo Android

- Modelo do dispositivo: 
- Versão do Android: 
- Arquitetura (arm64-v8a / armeabi-v7a / x86_64): 

## Contexto Adicional

Adicione qualquer outro contexto sobre o problema de atualização aqui.
