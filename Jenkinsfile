pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''python3 -m venv venv;
source venv/bin/activate;
pip install -r requirements.txt;'''
      }
    }

    stage('Configure') {
      steps {
        sh '''source venv/bin/activate;
cd martor_demo;
python manage.py makemigrations;
python manage.py migrate;
python manage.py test;

'''
      }
    }

    stage('UnitTest') {
      steps {
        sh '''source venv/bin/activate;
cd martor_demo;
python manage.py test;'''
      }
    }

    stage('Deploy') {
      steps {
        sh '''source venv/bin/activate;
cd martor_demo;
python manage.py check --deploy;
python manage.py collectstatic -c --noinput;'''
      }
    }

  }
}