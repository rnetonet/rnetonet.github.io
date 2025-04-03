+++
title = "Tratamento de Caracteres Especiais em Senhas com Flask-SQLAlchemy e psycopg2"
date = "2024-07-22"
draft = false
+++

## Contexto

Após passar muito tempo depurando um erro de conexão do Flask-SQLAlchemy com um banco de dados PostgreSQL,
descobri que a causa raiz era caracteres especiais na senha do banco de dados. Especificamente, a senha continha o símbolo `@`.

A mensagem de erro do **psycopg2** não foi muito útil, pois exibia um erro genérico:

```bash
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xd6 in position 61: invalid continuation byte
```

## Solução

Para resolver este problema, você deve escapar a senha usando **urllib.parse**:

```python
from urllib import parse
import psycopg2

dsn = fr"postgresql://souser:{parse.quote(password)}@localhost/test"
```

## Referências

*   https://stackoverflow.com/a/77193560
