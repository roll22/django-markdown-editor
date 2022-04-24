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
        sh '''containerName=django_dev;
docker stop $containerName || true && docker rm -f $containerName || true;
docker build -t django-markdown-editor .;
docker run --name $containerName -d -p 8020:8020      -e DJANGO_SUPERUSER_USERNAME=admin      -e DJANGO_SUPERUSER_PASSWORD=sekret1      -e DJANGO_SUPERUSER_EMAIL=admin@example.com      django-markdown-editor;
'''
      }
    }

  }
}