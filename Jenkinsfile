pipeline {
    agent any

    stages {
        stage('install-pip-deps') {
            steps {
                script{
                    build()
                }
            }
        }
        stage('deploy-to-dev') {
            steps {
                script{
                    deploy("dev", 7001)
                }
            }
        }
        stage('tests-on-dev') {
            steps {
                script{
                    test("dev")
                }
            }
        }
        stage('deploy-to-staging') {
            steps {
                script{
                    deploy("staging", 7002)
                }
            }
        }
        stage('tests-on-staging') {
            steps {
                script{
                    test("staging")
                }
            }
        }
        stage('deploy-to-preprod') {
            steps {
                script{
                    deploy("preprod", 7003)
                }
            }
        }
        stage('tests-on-preprod') {
            steps {
                script{
                    test("preprod")
                }
            }
        }
        stage('deploy-to-prod') {
            steps {
                script{
                    deploy("prod", 7004)
                }
            }
        }
        stage('tests-on-prod') {
            steps {
                script{
                    test("prod")
                }
            }
        }
    }
}

// for windows: bat "npm.."
// for linux/macos: sh "npm .."

def build(){
    echo "Building application is starting.."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git', changelog: false
    bat "dir"
    echo "Loading dependencies.."
    bat "pip install -r requirements.txt"
}

def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    echo "Cloning repo..."
    git branch: 'main', poll: false, url: 'https://github.com/mtararujs/python-greetings.git', changelog: false
    bat "pip install -r requirements.txt"

    echo "Deleting app..."
    bat "C:\\Users\\akosp\\AppData\\Roaming\\npm\\pm2 delete greeting-app-${environment} & EXIT /B 0"

    echo "Starting new app in environment:${environment}..."
    bat "C:\\Users\\akosp\\AppData\\Roaming\\npm\\pm2 start app.py --name greeting-app-${environment} -- --port ${port}"
}

def test(String environment){
    echo "Testing stage ${environment}"
    echo "cloning the repo..."
    git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mtararujs/course-js-api-framework.git'

    echo "Installing dependencies..."
    bat "npm install"

    echo "Running the tests..."
    bat "npm run greetings greetings_${environment}"
}