# Comparison Table

## ==
|     ==      | `true` | `false` |  `0`  | `''`  | `null` | `undefined` | `[]`  |  `{}`   |
|:-----------:|:------:|:-------:|:-----:|:-----:|:------:|:-----------:|:-----:|:-------:|
|   `true`    |   ⭕️   |  false  | false | false | false  |    false    | false |  false  |
|   `false`   | false  |   ⭕️    |  ⭕️   |  ⭕️   | false  |    false    |  ⭕️   |  false  |
|     `0`     | false  |   ⭕️    |  ⭕️   |  ⭕️   | false  |    false    |  ⭕️   |  false  |
|    `''`     | false  |   ⭕️    |  ⭕️   |  ⭕️   | false  |    false    |  ⭕️   |  false  |
|   `null`    | false  |  false  | false | false |   ⭕️   |     ⭕️      | false |  false  |
| `undefined` | false  |  false  | false | false |   ⭕️   |     ⭕️      | false |  false  |
|    `[]`     | false  |   ⭕️    |  ⭕️   |  ⭕️   | false  |    false    | false |  false  |
|    `{}`     | false  |  false  | false | false | false  |    false    | false | false ️ |

## ===
|     ===     | `true` | `false` |  `0`  | `''`  | `null` | `undefined` | `[]`  | `{}`  |
|:-----------:|:------:|:-------:|:-----:|:-----:|:------:|:-----------:|:-----:|:-----:|
|   `true`    |   ⭕️   |  false  | false | false | false  |    false    | false | false |
|   `false`   | false  |   ⭕️    | false | false | false  |    false    | false | false |
|     `0`     | false  |  false  |  ⭕️   | false | false  |    false    | false | false |
|    `''`     | false  |  false  | false |  ⭕️   | false  |    false    | false | false |
|   `null`    | false  |  false  | false | false |   ⭕️   |    false    | false | false |
| `undefined` | false  |  false  | false | false | false  |     ⭕️      | false | false |
|    `[]`     | false  |  false  | false | false | false  |    false    |  ⭕️   | false |
|    `{}`     | false  |  false  | false | false | false  |    false    | false |  ⭕ ️  |
