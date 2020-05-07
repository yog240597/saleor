# saleor-poc

Scoutandcellar is a e-commerce platform for wine shopping where customer can buy the product and the seller can sell their product
 
After all it is a platform where admin can manage consultant as well as customer. 

- Steps for making consultant in saleor :-



The Backend part is developed entirely using:-

- Python, Django, and some other required modules in backend (You may find list of base requirements under CODE_BASE/requirements.txt, 

:License: MIT

Terminology
-----------
CODE_BASE :- Reffers project’s this code root or base path where this document may also found out. May found out as, /scoutandcellar/backend


URLs & Structure
----------------

- Registration /api/v1/accounts/register/
    - First Name (required, alphanumeric / basic symbols)
    - Last name (required, alphanumeric / basic symbols)
    - Username (required, alphanumeric / basic symbols)
    - Email (email validations)
    - Mobile Number (required, alphanumeric / basic symbols, Complex mode)
    - Password (required,Password  character)
    - Confirm Password (required, Password  character, must be equal to Password)
- Login /api/v1/users/admin
    - Username (required, alphanumeric / basic symbols)
    - Password (required,Password  character, minlength: 8, maxlength:20)
- Login /api/v1/users/consultant
    - Username (required, alphanumeric / basic symbols)
    - Password (required,Password  character, minlength: 8, maxlength:20)
- Login /api/v1/users/customer
    - Username (required, alphanumeric / basic symbols)
    - Password (required,Password character, minlength: 8, maxlength:20)

- Login /api/v1/users/consultant/commission



Project Setup
-------------

Setting Up The Project Code
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Clone the frontend project with::

    $ git clone https://github.com/mirumee/saleor-dashboard.git   (for frontend)

    $ cd saleor-dashboard
    
    $ npm i

Add configuration:-

    set API_URI to: http://localhost:8000/graphql/

    set APP_MOUNT_URI to: http://localhost:9000/dashboard/

    set STATIC_URL to: http://localhost:9000/

Also add this url in API_URI in config.ts(6 line)

http://127.0.0.1:8000/graphql/

Start development server:-

    npm start


Clone the backend project with::    
    
    $ git clone https://github.com/mirumee/saleor.git   (for backend)

    $ cd saleor/

    $ pip install -r requirements.txt

    $ export SECRET_KEY='<mysecretkey>'

    Create a PostgreSQL user as mentioned below and create database

    $ python manage.py migrate

    $ npm install

    $ npm run build-assets

    $ npm run build-emails

    $ python manage.py runserver





May checkout::

    If in prduction then no need, but if latest changes are not on master but on ANY_OTHER_BRANCH then:-

    $ git checkout ANY_OTHER_BRANCH

Setting Up Database For Project On Current Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To setup a **PSQL Database on Ubuntu Bionic**, follow these steps::

    $ sudo apt update
    
    $ sudo apt install postgresql postgresql-contrib

    $  sudo -u postgres psql

    $ create database scoutandcellar;

    $  create user scoutandcellar_user with encrypted password 'scoutandcellar_password';

    $  grant all privileges on database scoutandcellar to scoutandcellar_user;

    $  \q


Setting Up PSQL Database Host
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    * If you are using db on same server, then you dont need need to change anything in backend code, else follow::

    $ sudo vim CODE_BASE/Dockerfile.production

    $ press "e" to edit

    - Find details with "database:"

    - Make the necessary changes as per database

    $ press "esc" to get back to vim command mode

    $ And with ":wq" save file with same name

Starting The Server 
^^^^^^^^^^^^^^^^^^^

There are two versions:- Production and Local. Go inside the CODE_BASE (ie. folder "scoutandcellar/backend/") and change text in between "production" and "local" as per requirements::

    $ cd CODE_BASE/

    $ sudo docker build -t scoutandcellar_backend -f Dockerfile.production ./

    $ sudo docker run -e env=production --net=host -p 8000:8000  --rm -it scoutandcellar_backend

If you ever get any problem please try with below command share the ss::

    $ sudo docker logs <Container ID (Returned by previous command)>

If its ever been need to be ran without Docker, follow::

    $ python3 -m venv ../env_scoutandcellar
    $ source ../env_scoutandcellar/bin/activate

    $ pip3 install -r requirements.txt 

    $ uvicorn main:app --reload --host 0.0.0.0 --port 8000
