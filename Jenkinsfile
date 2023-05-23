pipeline {
    agent any
    triggers{ pollSCM('*/1 * * * *') }

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
                    deploy("DEV", 1010)
                }
            }
        }
        stage('tests-on-dev') {
            steps {
                script{
                    test("BOOKS", "DEV")
                }
            }
        }
        stage('deploy-to-staging') {
            steps {
                script{
                    deploy("DEV", 1010)
                }
            }
        }
        stage('tests-on-staging') {
            steps {
                script{
                    test("BOOKS", "DEV")
                }
            }
        }
        stage('deploy-to-preprod') {
            steps {
                script{
                    deploy("DEV", 1010)
                }
            }
        }
        stage('tests-on-preprod') {
            steps {
                script{
                    test("BOOKS", "DEV")
                }
            }
        }
        stage('deploy-to-prod') {
            steps {
                script{
                    deploy("DEV", 1010)
                }
            }
        }
        stage('tests-on-prod') {
            steps {
                script{
                    test("BOOKS", "DEV")
                }
            }
        }
    }
}

// for windows: bat "npm.."
// for linux/macos: sh "npm .."

def build(){
    echo "Building of node application is starting.."
    git branch: 'master', poll: false, url: 'https://github.com/mtararujs/python-greetings.git'
    sh pip install -r requirements.txt
}

def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    bat "pm2 delete \"books-${environment}\""
    bat "pm2 start -n \"books-${environment}\" index.js -- ${port}"
}

def test(String test_set, String environment){
    echo "Testing ${test_set} test set on ${environment} has started.."
    bat "npm run ${test_set} ${test_set}_${environment}"
}