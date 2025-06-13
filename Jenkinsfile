pipeline{
    agent{
        label 'agent-1'
    }
    options{
        timeout(time:2 ,unit:'MINUTES')
        disableConcurrentBuilds()
    }
    environment {
        appVersion=''
        project= 'expense'
        environment='backend'
        ACC_ID='502141098545'
    }
    stages{
        stage('read version'){
            steps{
                 script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "Version is: $appVersion"
 
                }
            }
        }
        stage('dependencies'){
            steps{
                script{
                    sh """
                    npm install
                    """
                }
            }

        }
        stage('image build'){
            steps{
                script{
                    withAWS(region: 'us-east-1', credentials: 'd786594d-213c-45bb-9a84-9ae2a11b6b1d'){
                    sh """
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                    docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${project}/${environment}:${appVersion} .
                    docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${project}/${environment}:${appVersion}
 
                    """
                    }
                 
                }
            }
        }
            

    }  
}
    