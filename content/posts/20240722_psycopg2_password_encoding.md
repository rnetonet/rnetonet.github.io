+++
title = "Flask-SQLAlchemy, psycopg2 and passwords with special characters"
date = "2024-07-22"
draft = false
+++

# Flask-SQLAlchemy, psycopg2 and passwords with special characters

## Context

After spending a lot of time debugging a Flask-SQLAlchemy connection error to a PostgreSQL database, 
I found out the root cause was special characters in the database password. Specifically, the password contained the `@` symbol.

The **psycopg2** error message is not very helpful either, as it displays a generic error like:

```bash
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xd6 in position 61: invalid continuation byte
```

## Fixing

To fix it, you should escape the password using **urllib.parse**:

```python
from urllib import parse
import psycopg2

dsn = fr"postgresql://souser:{parse.quote(password)}@localhost/test"
```

## References

* https://stackoverflow.com/a/77193560