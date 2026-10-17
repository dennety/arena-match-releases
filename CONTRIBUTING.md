# Guia de Contribuição — ArenaMatch Releases

Este repositório é o canal de distribuição e atualização Over-The-Air (OTA) do aplicativo **ArenaMatch**. Ele hospeda o APK compilado, o manifesto `app_update.json` e a documentação pública.

O código-fonte do aplicativo cliente está no repositório separado: [dennety/arena_match](https://github.com/dennety/arena_match).

---

## Como Contribuir

### Reportar Problemas

Use o template de issue adequado:

- **Bug:** `Bug Report`
- **Melhoria/funcionalidade:** `Feature Request`
- **Problema de atualização OTA:** `OTA Update Issue`

### Enviar Alterações

1. Faça um fork deste repositório.
2. Crie uma branch a partir de `main`: `git checkout -b minha-mudanca`
3. Faça suas alterações e commit: `git commit -m "tipo(escopo): descrição"`
4. Envie a branch: `git push origin minha-mudanca`
5. Abra um Pull Request.

---

## Convenções de Commit

Este repositório segue [Conventional Commits](https://www.conventionalcommits.org/):

```
tipo(escopo): descrição
```

Tipos comuns:
- `feat`: nova funcionalidade
- `fix`: correção de bug
- `chore`: tarefa de manutenção (release, build, config)
- `docs`: alteração de documentação
- `refactor`: refatoração de código
- `test`: adição ou correção de testes

Exemplos:
- `chore(release): bump update manifest to v1.2.3 (build 6)`
- `fix(manifest): escape releaseNotes newlines in app_update.json`
- `docs(readme): add installation instructions and troubleshooting`

---

## Manifesto de Atualização (`app_update.json`)

Ao publicar uma nova versão, atualize os seguintes campos:

| Campo | Descrição |
|-------|-----------|
| `latestVersion` | Versão semântica (ex: `1.2.3`) |
| `latestBuildNumber` | Número do build (incrementar a cada release) |
| `minimumVersion` | Versão mínima do cliente compatível |
| `apkUrl` | URL do APK no GitHub Releases |
| `downloadHash` | SHA-256 do arquivo APK |
| `downloadSizeBytes` | Tamanho exato do APK em bytes |
| `fileSizeMb` | Tamanho em MB (para exibição) |
| `releaseNotes` | Changelog com quebras de linha escapadas (`\n`) |
| `forceUpdate` | `true` se a atualização for obrigatória |
| `updateType` | `feature`, `security`, `patch` |
| `publishedAt` | Data de publicação (ISO 8601 UTC) |

---

## Regras de Publicação

1. Não commite binários APK grandes diretamente sem Git LFS configurado.
2. Sempre valide o manifesto com `jq . app_update.json` antes de commitar.
3. Verifique a integridade do APK com `unzip -t ArenaMatch-release.apk`.
4. Crie uma tag Git para cada release: `git tag -a v1.2.3 -m "Release v1.2.3"`.

---

## Suporte

Para dúvidas sobre o aplicativo cliente (funcionalidades, bugs no app), abra issues no repositório [dennety/arena_match](https://github.com/dennety/arena_match).

Para dúvidas sobre atualizações OTA, download ou manifesto, abra issues neste repositório.
