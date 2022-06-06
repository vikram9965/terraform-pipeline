pipeline {
  agent any
  parameters {
    choice(
      name: 'Env',
      choices: ['Create', 'Destroy'],
      description: 'Passing the Environment'
    )
  }

  stages {
      stage('GIT_Clone') {
        steps {
        checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vikram9965/ec2-tf-infra.git']]]
           }
        }
        stage('Terraform_Setup') {
            steps {
                script {
                    if (params.Env == "Create") {
                       sh '''
                       echo "terraform create is in progress"
                       ls
                       terraform init -input=false
                       terraform apply --auto-approve -input=false
                       '''
                        
                    } else {
                       sh '''
                       echo "terraform destory is in progress"
                       terraform init -input=false
                       terraform destroy --auto-approve -input=false
                       '''                
                    }
                }
            }
        }
    
  }
}
