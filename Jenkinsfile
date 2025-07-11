#!groovy

//it means the libraries will be downloaded and accesible at run time
@Library('roboshop-library') _

def configMap = [
      application: 'nodeJSVM',
      component: 'catalogue'
]

// this is .groovy file name and function inside it
//if not master then trigger pipeline
if (! env.BRANCH_NAME.equalsIgnoreCase('master')){
      pipelineDecision.decidePipeline(configMap)
}
else{
      echo "master PROD deployment should happen through CR "
}