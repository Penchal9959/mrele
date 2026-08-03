# mrele

A Django storefront for an electronics retailer - product catalogue and detail pages.

Built with Django, Python, HTML and CSS.

> The original repository had a one-line README (`# mrele`) and no description; this one documents
> what the code actually does.

---

> **Archived.** This is early Django coursework from 2020-2021, kept for reference. It is no longer
> maintained. My current work is in GNSS signal processing and FPGA design - see my
> [profile](https://github.com/Penchal9959).

## Security note

This repository previously committed a Django `SECRET_KEY` in plaintext, and in some cases a
populated `db.sqlite3`. Those have been removed from the working tree and the key is now read from
the environment:

```python
SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY')
```

**They remain in the git history.** Treat the old key as compromised - it must never be reused.

## Running locally

```bash
python -m venv .venv && source .venv/bin/activate
pip install django
export DJANGO_SECRET_KEY="your-generated-secret-key"
python manage.py migrate
python manage.py runserver
```

## License

[MIT](LICENSE) (c) Penchalanarasaiah Kuncham