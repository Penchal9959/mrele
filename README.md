# mrele

A Django storefront for an electronics retailer: a product catalogue and a
detail page per product.

The repository name is an abbreviation of "MR Electronics". It is kept because
external links point at it.

> **Archived.** Early Django work from 2020-2021, kept as a record. Not
> maintained. Current work is GNSS signal processing and FPGA design - see the
> [profile](https://github.com/Penchal9959).

## What this was

Django, SQLite, server-rendered templates, static product imagery. A `Product`
model, a list view and a detail view. The original repository had a one-line
README (`# mrele`) and no description; this one records what the code does.

## Security

A Django `SECRET_KEY` was committed to this repository in plaintext; two different keys, across two commits.
**Both have since been purged from the entire history**, not merely deleted at
`HEAD`, and the purge was verified by scanning every object in a fresh clone.

Treat the old key as compromised regardless. A value that has been public stays
public; removing it stops future discovery, not past discovery.

The key now comes from the environment with **no fallback**:

```python
SECRET_KEY = os.environ['DJANGO_SECRET_KEY']
```

Subscript access, not `.get()`. An application that starts on a publicly known
default is worse than one that refuses to start.

Nine compiled `.pyc` files and three `.DS_Store` files were also committed and
have been purged. `mysite/__pycache__/settings.cpython-39.pyc` mattered more
than the rest: compiled Python keeps string constants, so it carried the key
too.

## Configuration

Settings come from the environment, not from `settings.py`.

```sh
cp .env.example .env      # then edit .env
```

| Variable | Required | What it is |
|---|---|---|
| `DJANGO_SECRET_KEY` | yes | Signs sessions, password-reset tokens and CSRF tokens. Startup raises `KeyError` if unset |
| `DJANGO_DEBUG` | no | `true` enables debug. Anything else, including unset, leaves it off |
| `ALLOWED_HOSTS` | no | Comma-separated. Defaults to `localhost,127.0.0.1` |

`.env` is in `.gitignore`.

## Running locally

```sh
python -m venv .venv && source .venv/bin/activate
pip install django
cp .env.example .env          # then set DJANGO_SECRET_KEY in it
export $(grep -v '^#' .env | xargs)
python manage.py migrate
python manage.py runserver
```

## Known limitations

- No cart, no checkout, no payment. It is a catalogue, not a shop.
- `ALLOWED_HOSTS` was `["*"]`, which accepts any `Host` header. It now reads
  from the environment and defaults to localhost.
- No tests.

## Licence

[MIT](LICENSE) (c) Penchalanarasaiah Kuncham
