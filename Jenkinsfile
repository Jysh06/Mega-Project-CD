pipeline {
    agent any

    stages {
        stage('GIT CHECKOUT') {
            steps {
                git branch: 'main', url: 'https://github.com/Jysh06/Mega-Project-CD.git'
            }
        }
        
         stage('KUBERNETES DEPLOYMENT') {
            steps {
                 withKubeConfig(caCertificate: '', clusterName: ' devopsshack-cluster', contextName: '', credentialsId: 'kube-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://30463FF1838D6D7CDC46BBC14DCA266D.gr7.ap-south-1.eks.amazonaws.com') {
                    sh 'kubectl apply -f Manifest/manifest.yaml -n webapps'
                    sh 'kubectl apply -f Manifest/HPA.yaml -n webapps'
                    sh '''
                        kubectl get pods -n webapps
                        kubectl get svc -n webapps
                        kubectl get deploy -n webapps
                        kubectl get hpa -n webapps
                       '''
                }
            }
        }
    }
}
