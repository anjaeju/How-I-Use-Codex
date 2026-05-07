## 이슈 1) Codex VSCode Extension Crash 해결 기록

### 문제 상황
- Codex에서 Ouroboros를 포함해 여러 custom skill / MCP / agent 설정을 추가해서 사용하던 중, **Visual Studio Code Extension에서만 Codex가 정상 실행되지 않는 문제**가 발생했다.
- Codex CLI 또는 다른 환경에서는 문제가 명확하지 않았지만, VSCode Extension에서는 Codex 프로세스가 바로 죽거나 연결되지 않았다.

### 에러 메시지
```text
Codex crashed with the following error:

Codex process errored: Codex process is not available
dropping overload response for connection ConnectionId(0): outbound queue is full
```
- Ouroboros 및 여러 custom skill / MCP / agent 설정을 동시에 붙여서 사용하면서 Codex 설정이 복잡해졌고, VSCode Extension 초기화 과정에서 일부 설정이 충돌하거나 불안정하게 동작한 것으로 보인다.
- 특히 `config.toml`의 `approvals_reviewer` 설정이 문제와 관련되어 있었다.

### 해결 방법
`config.toml`에서 아래 설정을 적용했다.
```toml
# approvals_reviewer = "guardian_subagent"
approvals_reviewer = "auto_review" or "user"
```
- 설정 변경 후 VSCode에서 Codex Extension을 Reload 하니 다시 정상 동작했다.

### 정리
- 이번 문제는 Codex 자체 기능 문제라기보다는, Ouroboros / custom skill / MCP / agent 설정을 여러 개 붙이는 과정에서 VSCode Extension 쪽 초기화가 불안정해진 케이스로 보인다.
- 비슷한 문제가 다시 발생하면 아래 순서로 확인한다.
```text
1. `config.toml`에서 최근 추가한 custom skill / MCP / agent 설정 확인
2. `approvals_reviewer` 설정 확인
3. VSCode Codex Extension Reload
4. 그래도 안 되면 Ouroboros 또는 MCP 서버를 하나씩 비활성화하면서 원인 분리
```
