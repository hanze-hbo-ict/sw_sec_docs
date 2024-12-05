Do not forget to first make and activate a virtual environment (e.g. ``python -m venv myvenv``, ``myvenv\Scripts\activate``).
If you use PowerShell and ``activate`` does not work, first type in the following command: ``Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned``

Then install some essential packages: ``pip install flask flask-wtf flask-sqlalchemy flask-login``.

Then run make_db **once** to create and seed the DB: ``python make_db.py``

Finally, run the app: ``python app.py``