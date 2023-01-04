pipeline {

    agent {
     label 'python'
   }
     environment {
    HARBOR_CREDENTIAL_ID = 'harbor-id'
    REGISTRY = '172.30.102.24:30002'
    HARBOR_NAMESPACE = 'library'
    APP_NAME = 'demo-go-lang-app'
     }
    
    stages {
        stage('Build') {
            agent {
                docker {
                    
                    image 'python:2-alpine'
                }
            }
            steps {
                
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Test') {
            agent {
                docker {
                   
                    image 'qnib/pytest'
                }
            }
            steps {
                
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                   
                    junit 'test-reports/results.xml'
                }
            }
        }
        
                    
                    
        }
    }
}
        
           
        
       
  
