pipeline {
    agent any

tools {
    maven 'maven3'
}

options{
    buildDiscarder(logRotator(numToKeepStr:'3'))
    retry(3)
    timestamps()
}

parameters{
    string(name: "branch", defaultValue: "main", description: "select the branch")
    choice(name: "Environment", choices: "dev\ntest\nprod", description: "select the environment")
}

stages {
    stage("pull code"){
        steps {
            git branch: 'main', credentialsId: 'git_pass', url: 'https://github.com/sand9989/san-demo-app.git'
        }
    }

    stage("maven deploy"){
        // when { ${params.Environment} == "dev"}
        steps{
            sh "mvn clean"
        }
    }

    stage("maven test report"){
        steps{
            sh "mvn surefire-report:report"
        }
    }
}
}
