# Plano de Implementação — Amanhã (ArenaMatch)

**Data:** Amanhã  
**Repositório alvo:** `dennety/arena_match` (código-fonte do app cliente)  
**Issues a implementar:** #2 (wakelock timeout) e #3 (confirmação de partida)  
**Issues deixados para depois:** #1 (split APK — requer mudança de build system, mais complexo)

---

## 🎯 Objetivo do Dia

Implementar duas melhorias de alta prioridade que evitam problemas de UX e economia de bateria:

1. **Issue #3:** Confirmação antes de finalizar partida + botão "Desfazer" na Súmula Ultra-Rápida
2. **Issue #2:** Timeout automático do wakelock + alerta de bateria baixa no modo Rei da Quadra

---

## 📋 Pré-requisitos (faça hoje à noite)

- [ ] Clone o repositório `dennety/arena_match` localmente
- [ ] Verifique que o Flutter está instalado: `flutter --version`
- [ ] Verifique que consegue rodar o app: `flutter run` (em emulador ou dispositivo físico)
- [ ] Crie uma branch: `git checkout -b melhorias-ux-bateria`
- [ ] Leia o código atual da Súmula Ultra-Rápida e do modo Rei da Quadra para entender a estrutura

---

## ⏰ Cronograma Estimado (8 horas)

| Horário | Tarefa | Issue |
|---------|--------|-------|
| 09:00–09:30 | Preparação e leitura do código | Ambas |
| 09:30–12:00 | Implementar confirmação de partida + desfazer | #3 |
| 12:00–13:00 | Almoço | — |
| 13:00–15:30 | Implementar timeout wakelock + alerta bateria | #2 |
| 15:30–16:30 | Testes manuais em dispositivo/emulador | Ambas |
| 16:30–17:00 | Build APK de teste e commit | Ambas |

---

## 🔧 Tarefa 1 — Confirmação de Partida + Desfazer (Issue #3)

**Onde:** Tela de Súmula / Registro de gols (arquivos Dart da feature de súmula)  
**Tempo:** 2.5 horas  
**Complexidade:** Baixa–Média

### Passos

1. **Localizar o botão/action de "finalizar partida"**
   - Busque por funções como `finalizarPartida`, `endMatch`, `finalizarSúmula`, ou similar no código Dart
   - Verifique onde é chamado o salvamento do placar no banco local (provavelmente SQLite ou Hive/Isar)

2. **Adicionar diálogo de confirmação**
   ```dart
   // Exemplo de estrutura (adapte ao seu código)
   Future<void> _confirmarFinalizacao() async {
     final confirmado = await showDialog<bool>(
       context: context,
       builder: (context) => AlertDialog(
         title: Text('Finalizar partida?'),
         content: Text('Esta ação não poderá ser desfeita.'),
         actions: [
           TextButton(
             onPressed: () => Navigator.pop(context, false),
             child: Text('Cancelar'),
           ),
           ElevatedButton(
             onPressed: () => Navigator.pop(context, true),
             child: Text('Sim, finalizar'),
           ),
         ],
       ),
     );
     if (confirmado == true) {
       await _salvarPartida();
     }
   }
   ```

3. **Adicionar botão "Desfazer" (últimos 10 segundos)**
   - Após finalizar, mostrar um Snackbar com ação "Desfazer" por 10 segundos
   - Se o usuário tocar em "Desfazer", excluir a partida recém-criada e voltar ao placar anterior
   ```dart
   ScaffoldMessenger.of(context).showSnackBar(
     SnackBar(
       content: Text('Partida finalizada'),
       action: SnackBarAction(
         label: 'Desfazer',
         onPressed: () async {
           await _desfazerUltimaPartida();
         },
       ),
       duration: Duration(seconds: 10),
     ),
   );
   ```

4. **Critério de conclusão**
   - [ ] Ao tentar finalizar, aparece diálogo de confirmação
   - [ ] Cancelar no diálogo não fecha a partida
   - [ ] Confirmar fecha a partida e mostra Snackbar "Desfazer"
   - [ ] Tocar em "Desfazer" dentro de 10s reabre a partida anterior

---

## 🔋 Tarefa 2 — Timeout Wakelock + Alerta Bateria (Issue #2)

**Onde:** Tela do modo Rei da Quadra (arquivos Dart da feature King of the Court)  
**Tempo:** 2.5 horas  
**Complexidade:** Baixa–Média

### Passos

1. **Localizar onde o wakelock é ativado**
   - Busque por `wakelock_plus`, `NoSleep`, `enable`, `WakeLock.enable()` no código
   - Identifique o ponto exato de ativação (provavelmente ao entrar na tela Rei da Quadra)

2. **Adicionar timeout automático**
   - Use um `Timer` para desativar o wakelock após X minutos sem interação (sugestão: 5 minutos)
   - Resetar o timer a cada interação do usuário (toque na tela, atualização de placar)
   ```dart
   Timer? _wakelockTimer;

   void _resetWakelockTimer() {
     _wakelockTimer?.cancel();
     _wakelockTimer = Timer(Duration(minutes: 5), () async {
       await WakeLock.disable();
       _mostrarAlerta('Wakelock desativado por inatividade');
     });
   }
   ```

3. **Adicionar alerta de bateria baixa**
   - Use o pacote `battery_plus` (ou similar já presente no pubspec) para monitorar nível de bateria
   - Quando bateria < 20% e wakelock ativo, mostrar alerta
   ```dart
   final bateria = await Battery().batteryLevel;
   if (bateria < 20 && wakelockAtivo) {
     showDialog(
       context: context,
       builder: (_) => AlertDialog(
         title: Text('Bateria baixa'),
         content: Text('O wakelock está ativo e pode drenar a bateria. Deseja desativar?'),
         actions: [
           TextButton(onPressed: () => Navigator.pop(context), child: Text('Manter ativo')),
           ElevatedButton(
             onPressed: () async {
               await WakeLock.disable();
               Navigator.pop(context);
             },
             child: Text('Desativar wakelock'),
           ),
         ],
       ),
     );
   }
   ```

4. **Critério de conclusão**
   - [ ] Wakelock desativa automaticamente após 5 min sem interação
   - [ ] Timer reseta quando o usuário interage com o placar
   - [ ] Alerta aparece quando bateria < 20% com wakelock ativo
   - [ ] Usuário pode escolher desativar wakelock pelo alerta

---

## 📱 Tarefa 3 — Testes Manuais (Ambas)

**Tempo:** 1 hora

- [ ] Abrir o app em emulador ou dispositivo físico
- [ ] Navegar até modo Rei da Quadra e verificar wakelock ativo
- [ ] Aguardar/simular inatividade e verificar se wakelock desativa após timeout
- [ ] Simular bateria baixa e verificar se alerta aparece
- [ ] Fazer uma partida na Súmula, finalizar, verificar diálogo de confirmação
- [ ] Tocar em "Desfazer" no Snackbar e verificar se partida é revertida
- [ ] Tocar em "Cancelar" no diálogo e verificar que partida continua aberta

---

## 🏗️ Tarefa 4 — Build e Commit (se tudo passar)

**Tempo:** 30 min

```bash
# No repositório dennety/arena_match
flutter build apk --release --split-per-abi

# Verificar tamanho dos APKs gerados
ls -la build/app/outputs/flutter-apk/

# Commit
git add .
git commit -m "feat(ux): confirmação de partida, desfazer e timeout wakelock"
```

---

## ✅ Checklist de Conclusão

- [ ] Issue #3 implementada: confirmação + desfazer funcionando
- [ ] Issue #2 implementada: wakelock timeout + alerta bateria funcionando
- [ ] App compila sem erros: `flutter build apk --release` sem falhas
- [ ] Testes manuais aprovados em dispositivo/emulador
- [ ] Commit criado na branch `melhorias-ux-bateria`

---

## 📅 Próximos Passos (após amanhã)

| Issue | Quando | Observação |
|-------|--------|------------|
| #1 — Split APK / App Bundle | Próxima semana | Requer mudança no `build.gradle` ou uso de `.aab` |
| #4 — Código de convite ligas | Próxima sprint | Nova feature de backend local |
| #5 — Criptografia backup JSON | Próxima sprint | Segurança de dados locais |
| #6 — Preview cards sociais | Próxima sprint | UI/UX do gerador de cards |
| #7 — Duplicados importador WhatsApp | Backlog | Melhoria de parsing |

---

## 📄 Arquivos para Adaptar (caminhos típicos Flutter)

Adapte conforme a estrutura real do seu projeto:

- `lib/src/features/sumula/` — lógica da súmula ultra-rápida
- `lib/src/features/king_of_the_court/` — modo Rei da Quadra
- `lib/src/services/wakelock_service.dart` — se existir serviço de wakelock
- `pubspec.yaml` — para adicionar `battery_plus` se ainda não tiver

---

**Dica:** Se não conseguir terminar ambas as tarefas amanhã, priorize a **Issue #3 (confirmação de partida)** — é a mais rápida de implementar e evita um erro real de usuário (finalização acidental).
