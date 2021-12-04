# Logback effective levels
- http://logback.qos.ch/manual/architecture.html
- https://www.tutorialspoint.com/log4j/log4j_logging_levels.htm

| Level | Description              |
|-------|--------------------------|
| ALL   | 커스텀 레벨을 포함한 모든 레벨        |
| TRACE | DEBUG보다 상세               |
| DEBUG | 디버그                      |
| INFO  | 프로그램의 동작 상태, 진행 상황 등의 정보 |
| WARN  | 잠재적인 위험에 대한 경고           |
| ERROR | 오류                       |
| FATAL | 프로그램이 중단될 수 있는 심각한 오류    |
| OFF   | 해제                       |

| Config \ Event | TRACE | DEBUG | INFO | WARN | ERROR | FATAL |
|----------------|-------|-------|------|------|-------|-------|
| ALL            | O     | O     | O    | O    | O     | O     |
| TRACE          | O     | O     | O    | O    | O     | O     |
| DEBUG          |       | O     | O    | O    | O     | O     |
| INFO           |       |       | O    | O    | O     | O     |
| WARN           |       |       |      | O    | O     | O     |
| ERROR          |       |       |      |      | O     | O     |
| FATAL          |       |       |      |      |       | O     |
| OFF            |       |       |      |      |       |       | 
