# ⚽ ArenaMatch — Releases Oficiais do APK

<div align="center">
  <img src="https://raw.githubusercontent.com/dennety/arena_match/main/assets/icons/app_icon.png" width="140" alt="ArenaMatch Icon" />
  <br />
  <strong>Gestor de Ligas Privadas, Rei da Quadra, Placar Esportivo & Cards Sociais</strong>
  <br /><br />
  <a href="https://github.com/dennety/arena-match-releases/releases/latest/download/ArenaMatch-release.apk">
    <img src="https://img.shields.io/badge/Download-ArenaMatch_APK-00E5FF?style=for-the-badge&logo=android&logoColor=black" alt="Baixar APK" />
  </a>
</div>

---

### 📲 Atualizações Automáticas (OTA)

O **ArenaMatch** possui um motor nativo de auto-atualização integrado. Quando uma nova versão é publicada neste repositório:

1. O aplicativo detecta a versão automaticamente ao abrir ou pelo botão na barra superior.
2. Exibe o changelog completo com as novidades.
3. Faz o download em segundo plano com indicador de progresso em tempo real.
4. Aciona a instalação do APK nativamente sem requerer Google Play Store.

---

### 📥 Download Direto

- **Última Versão:** [Baixar ArenaMatch-release.apk](https://github.com/dennety/arena-match-releases/releases/latest/download/ArenaMatch-release.apk)
- **Versão:** `1.2.2` (build 5)
- **Tamanho:** `56.35 MB` (`59.087.668 bytes`)
- **Manifesto de Atualização:** [`app_update.json`](app_update.json)
- **Hash SHA-256:** `a89800df0df705f73070a84012908f42b43784ff9c0f047563b92e3cfb3c54ea`

---

### 🛠️ Como Instalar o APK Manualmente

Como o ArenaMatch não está na Google Play Store, a instalação é feita via **APK direto (sideloading)**:

#### No Android

1. **Baixe o APK** pelo link acima ou diretamente no app (atualização OTA).
2. **Habilite fontes desconhecidas:**
   - Vá em **Configurações > Apps > ArenaMatch > Permitir instalar apps desconhecidos** (ou **Configurações > Segurança > Fontes desconhecidas**, dependendo da versão do Android).
   - Ative a opção para o navegador ou gerenciador de arquivos que você usará.
3. **Abra o arquivo APK** baixado e toque em **Instalar**.
4. Após a instalação, abra o app e faça login ou crie sua liga privada.

> ⚠️ O APK é assinado com a chave de release do ArenaMatch. Não modifique o arquivo após o download.

---

### 🛡️ Funcionalidades Principais

- 👑 **Modo Rei da Quadra (King of the Court):** Rotação sequencial estrita FIFO, placar landscape com *wakelock* (tela sempre acesa).
- 🏆 **Ligas Privadas & Temporadas:** Classificação por vitórias, saldo de gols/pontos e eleição algorítmica de MVP, Artilheiro e Curinga.
- 📸 **Gerador de Cards Sociais 9:16:** Criação instantânea de stories para WhatsApp e Instagram com fotos reais da pelada e humor esportivo.
- 💬 **Importador Inteligente do WhatsApp:** Parsing com detecção de nomes, posições e notas por estrelas (`⭐⭐⭐`).
- ⚡ **Súmula Ultra-Rápida:** Registro de gols e finalização em menos de 5 segundos (< 3 toques).
- 💾 **Privacidade Local-First:** 100% dos dados salvos no aparelho, com backup/restauração em JSON.

---

### ⚠️ Permissões e Impacto na Bateria

O ArenaMatch utiliza as seguintes funcionalidades sensíveis:

| Recurso | Uso | Impacto |
|---------|-----|---------|
| **Wakelock** (tela sempre acesa) | Modo Rei da Quadra — mantém o placar visível durante jogos | Pode drenar a bateria mais rápido durante uso prolongado |
| **Armazenamento local** | Salvamento de dados, backup e restauração em JSON | Nenhum dado enviado para nuvem externa |
| **Câmera / Galeria** | Geração de cards sociais com fotos da pelada | Apenas para criar as imagens compartilhadas |

> 💡 **Dica:** Desative o modo Rei da Quadra quando não estiver jogando para economizar bateria.

---

### 🐛 Solução de Problemas (Troubleshooting)

| Problema | Possível Causa | Solução |
|----------|---------------|---------|
| O app não detecta atualização | Manifesto OTA não acessível ou versão incompatível | Verifique sua conexão com a internet e reinicie o app |
| Falha ao instalar o APK | "Fontes desconhecidas" não habilitado | Vá em Configurações > Apps e permita instalação de fontes desconhecidas |
| Download interrompeu | Conexão instável ou espaço insuficiente | Verifique o espaço disponível no dispositivo e tente novamente |
| APK corrompido | Download incompleto | Baixe novamente e compare o SHA-256: `a89800df...` |
| App fecha ao abrir | Versão do Android incompatível | O app requer Android 5.0 (API 21) ou superior |
| Bateria drena rápido | Wakelock ativo no modo Rei da Quadra | Desative o modo quando não estiver jogando |

---

### 📋 Requisitos do Sistema

- **Android:** 5.0 (API 21) ou superior
- **Arquiteturas suportadas:** arm64-v8a, armeabi-v7a, x86_64
- **Espaço livre:** mínimo 60 MB

---

### 🔒 Segurança

- O manifesto de atualização inclui hash SHA-256 para verificação de integridade do APK.
- Todas as atualizações são baixadas via HTTPS.
- Dados do usuário permanecem no dispositivo (privacidade local-first).

---

### 📄 Licença

Consulte o arquivo [`LICENSE`](LICENSE) para os termos de uso.
