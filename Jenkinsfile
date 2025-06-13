pipeline{
    agent{
        label 'agent-1'
    }
    options{
        timeout(time:2 ,unit:'MINUTES')
        disableConcurrentBuilds()
    }
    envionment {
        appVersion=''
        project= 'expense'
        environment='dev'
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
    }  
}
    