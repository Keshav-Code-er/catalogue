pipeline{
       agent { node { label 'Agent-1' } }
       stages {
            stage('Install dependencies'){
                  steps{
                        sh 'npm install'
                  }
            }

            stage('Unit test'){
                  steps {
                        echo "unit testing is done here"
                  }
            }
       }
}
