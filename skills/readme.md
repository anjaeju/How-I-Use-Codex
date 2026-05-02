
## Ouroboros
- Ouroboros is a workflow/harness-style approach that can help Claude or Codex to run predefined internal commands and generate structured outputs.
- 체감상 20-30% 정도의 완성도가 올라갔으며, 특히 ooo interview 기능이 (다른 하네스 기능의 interview) 보다 상세하고 핵심이다.
- 또한, Seed 파일을 만들어서 제작이 들어가는 것이 매우 우수함. (간단한 Task는 바로 구현에 들어가서 복잡하지 않음)
- 아래와 같은 flow로 거의 사용하려고한다.
```text
[pre-defined config, however; mostly skip]
        ↓
ooo interview
        ↓
[seed YAML generated]
        ↓
ooo run seed/xxx.yaml
        ↓
[outputs generated]
```
