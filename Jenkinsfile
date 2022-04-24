pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh '''ls;
python3 -m venv venv;
source venv/bin/activate;
pip install -r requirements.txt;
python manage.py makemigrations;
python manage.py migrate;
python manage.py test;
python manage.py check --deploy;
python manage.py collectstatic;
python manage.py runserver;
'''
      }
    }

  }
}