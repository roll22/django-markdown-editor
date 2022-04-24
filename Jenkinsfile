pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''python3 -m venv venv;
source venv/bin/activate;'''
        sh 'pip install -r requirements.txt;'
      }
    }

    stage('Configure') {
      steps {
        sh '''cd martor_demo;
python manage.py makemigrations;
python manage.py migrate;
python manage.py test;
python manage.py check --deploy;
python manage.py collectstatic -c --noinput;
python manage.py runserver;
'''
      }
    }

  }
}