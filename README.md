```bash
curl 'http://localhost:8080/run_code' \
  -H 'Content-Type: application/json' \
  --data-raw '{
    "language": "lean",
    "code": "def add (a b : Nat) : Nat := a + b\n#eval add 20 22",
    "compile_timeout": 10,
    "run_timeout": 10
  }'
```
