pipeline{
       agent { node { label 'Agent-1' } }
       environment{
            //here if you create any variable you will have global access, since it is environment no need of def 
            packageVersion = ''
       }
       stages {
            stage('Get Version'){
                  steps{
                     script{
                        def packageJson = readJSON file: 'package.json'
                        packageVersion = packageJson.version
                        echo "version: ${packageVersion}"
                     }
                  }
            }
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
            //sonar-scanner command  expect sonar-project.properties should be available
            stage('Sonar Scan'){
                  steps {
                        echo "Sonar scan done"
                  }
            }

            stage('Build'){
                  steps {
                        sh 'ls -ltr'
                        sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
                        
                  }
            }

               stage('SAST'){
                  steps {
                       echo "SAST Done"
                        
                  }
            }

            //install pipeline utility steps plugin, if not installed

             stage(' Publish Artifact'){
                  steps {
                        nexusArtifactUploader(
                              nexusVersion: 'nexus3',
                              protocol: 'http',
                              nexusUrl: '34.207.166.144:8081/',
                              groupId: 'com.roboshop',
                              version: "$packageVersion",
                              repository: 'catalogue',
                              credentialsId: 'nexus-auth',
                              artifacts: [
                                    [artifactId: 'catalogue',
                                    classifier: '',
                                    file: 'catalogue.zip',
                                    type: 'zip']
            ]
     )
                       
                        
                  }
            }

            // here I need to configure downstream job. I have to pass packages version for deployment
            // This job will wait until downstream job is over
             stage('Deploy'){
                  steps {
                        echo 'Deployment'
                        build job: "../catalogue-deploy", wait: true
                  }
            }
       }

       post{
            always{
                  echo 'cleaning up workspace'
                  deleteDir()
            }
       }
}
