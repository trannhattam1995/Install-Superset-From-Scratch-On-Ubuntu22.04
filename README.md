# How to install Superset from scratch on Ubuntu 22.04

```bash
sudo apt-get install build-essential libssl-dev libffi-dev python3-dev python3-pip libsasl2-dev libldap2-dev default-libmysqlclient-dev
```

```bash
sudo apt install python3.10-venv
```

```bash
python3 -m venv venv
```

```bash
. venv/bin/activate
```

```bash
pip install wheel
```

```bash
pip install flask-wtf==0.14.2
pip install flask==1.1.0
pip install werkzeug==0.16.1
```

```bash
pip install apache-superset
```

```bash
export FLASK_APP=superset
```

```bash
openssl rand -base64 42
```

Edit the SECRET_KEY value with above value.
Edit the SQLALCHEMY_DATABASE_URI. Default value ~/.superset/superset.db
If the error exists check the permission of the superset.db file.
If the file not exists use the following command to create the file.

```bash
sudo cd /home/user/.superset
sqlite superset.db
sudo chmod 777 /home/user/.superset/superset.db
```

```bash
export SUPERSET_CONFIG_PATH=/app/superset_config.py
```

```text
# Superset specific config
ROW_LIMIT = 5000

# Flask App Builder configuration
# Your App secret key will be used for securely signing the session cookie
# and encrypting sensitive information on the database
# Make sure you are changing this key for your deployment with a strong key.
# Alternatively you can set it with `SUPERSET_SECRET_KEY` environment variable.
# You MUST set this for production environments or the server will not refuse
# to start and you will see an error in the logs accordingly.
SECRET_KEY = 'YOUR_OWN_RANDOM_GENERATED_SECRET_KEY'

# The SQLAlchemy connection string to your database backend
# This connection defines the path to the database that stores your
# superset metadata (slices, connections, tables, dashboards, ...).
# Note that the connection information to connect to the datasources
# you want to explore are managed directly in the web UI
# The check_same_thread=false property ensures the sqlite client does not attempt
# to enforce single-threaded access, which may be problematic in some edge cases
SQLALCHEMY_DATABASE_URI = 'sqlite:////path/to/superset.db?check_same_thread=false'

# Flask-WTF flag for CSRF
WTF_CSRF_ENABLED = True
# Add endpoints that need to be exempt from CSRF protection
WTF_CSRF_EXEMPT_LIST = []
# A CSRF token that expires in 1 year
WTF_CSRF_TIME_LIMIT = 60 * 60 * 24 * 365

# Set this API key to enable Mapbox visualizations
MAPBOX_API_KEY = ''
```

```bash
superset db upgrade
```

Create admin. Remeber let admin username to admin to make the next command work well.

```bash
superset fab create-admin
```

Load sample data.

```bash
superset load_examples
```

Create default roles and permissions

```bash
superset init
```

To start a development web server on port 8088, use -p to bind to another port

```bash
superset run -p 8088 --with-threads --reload --debugger
```
