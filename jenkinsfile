pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/srcb-aws/traffic-file.git'
            }
        }

        stage('Install Python & Create Virtual Env') {
            steps {
                sh '''
                sudo yum update -y
                sudo yum install -y python3 python3-pip mesa-libGL

                python3 -m venv ${VENV_DIR}
                source ${VENV_DIR}/bin/activate

                pip install --upgrade pip
                pip install flask opencv-python ultralytics
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                source ${VENV_DIR}/bin/activate
                python3 app.py
                '''
            }
        }
    }
}
