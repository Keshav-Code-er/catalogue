#!groovy

//it means the libraries will be downloaded and accesible at run time
@Library('roboshop-library') _

def configMap = [
      application: 'nodeJSVM',
      component: 'catalogue'
]

// this is .groovy file name and function inside it
pipelineDecision.decidePipeline(configMap)
