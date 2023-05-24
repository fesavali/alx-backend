If you look in the terminal session where the application is running, you will see a stack trace of the error. Stack traces are extremely useful in debugging errors, because they show the sequence of calls in that stack, all the way to the line that produced the error:

(venv) $ flask run
 * Serving Flask app "microblog"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
[2021-06-14 22:40:02,027] ERROR in app: Exception on /edit_profile [POST]
Traceback (most recent call last):
  File "venv/lib/python3.6/site-packages/sqlalchemy/engine/base.py", in _execute_context
    context)
  File "venv/lib/python3.6/site-packages/sqlalchemy/engine/default.py", in do_execute
    cursor.execute(statement, parameters)
sqlite3.IntegrityError: UNIQUE constraint failed: user.username
The stack trace indicates what is the bug. The application allows a user to change the username, and does not validate that the new username chosen does not collide with another user already in the system. The error comes from SQLAlchemy, which tries to write the new username to the database, but the database rejects it because the username column is defined with unique=True.

It is important to note that the error page that is presented to the user does not provide much information about the error, and that is good. I definitely do not want users to learn that the crash was caused by a database error, or what database I'm using, or what are some of the table and field names in my database. All that information should be kept internal.