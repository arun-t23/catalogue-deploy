pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        COURSE  =   "Jekins"
        appVersion  =   ""
        ACC_ID      =   "611669940532"
        PROJECT     =   "roboshop"
        COMPONENT   =   "catalogue"
    }
    options {
        timeout(time: 30, unit: 'Minutes')
        disableConcurrentBuild()
    }
    parameters  {
        string(name: 'appVersion', description: 'which app version do you want to deploy')
        choice(name: 'deploy_to', choices: ['dev', 'qa', 'prod'], description: 'pick something')
    }
    // This is build section
    Stages  {
        stage   {
            steps   {
                scrpit  {
                    withAWS(region:'us-east-1',credentials:'aws-creds') {
                        sh """
                            aws eks update-kubeconfig --region ${REGION} --name ${PROJECT}-${params.deploy_to}
                        """
                    }
                }
            }

        }
    }
    post    {
        
       always{
                echo 'I will always say Hello again!'
                cleanWs()
            }
            success{
                echo 'I will run if success'
            }
            failure{
                echo 'I will run if failing'
            }
            aborted{
                echo 'Pipeline is aborted'
            } 
    }
}