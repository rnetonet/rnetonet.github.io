+++
title = "Handling Special Characters in Passwords with Flask-SQLAlchemy and psycopg2"
date = "2024-07-22"
draft = false
+++

## Context

After spending a lot of time debugging a Flask-SQLAlchemy connection error to a PostgreSQL database, 
I discovered that the root cause was special characters in the database password. Specifically, the password contained the `@` symbol.

The **psycopg2** error message was not very helpful, as it displayed a generic error:

```bash
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xd6 in position 61: invalid continuation byte
```

## Solution

To resolve this issue, you should escape the password using **urllib.parse**:

```python
from urllib import parse
import psycopg2

dsn = fr"postgresql://souser:{parse.quote(password)}@localhost/test"
```

## References

* https://stackoverflow.com/a/77193560