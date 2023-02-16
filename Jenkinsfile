pipeline {
    agent any
    stages {
       stage("Generating OIDC token and saving it to a file") {
            steps {
                script {
                        sh (script: 'sudo gcloud auth print-identity-token first-service-account@flawless-helper-376817.iam.gserviceaccount.com  --audiences="//iam.googleapis.com/projects/1048415450475/locations/global/workloadIdentityPools/jenkins/providers/jenkins"  > /usr/share/token/key/credential.key',returnStdout: true)
                }
            }
        }
        stage ("getting the WIF config file into a variable")
        {
            steps {
                     withCredentials([file(credentialsId: 'wif', variable: 'WIF')]) 
                        {
                         sh '''
                            gcloud auth login --brief --cred-file=$WIF --quiet
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
