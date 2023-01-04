pipeline {

    agent{
        label (python)
    }
    stages {
        stage('Build') {
            steps {
                container ('python') {
                   sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                   stash(name: 'compiled-results', includes: 'sources/*.py*')
                }
               
            }
        }
                   
              
        stage('Test') {
            agent {
                docker {
                    //This image parameter downloads the qnib:pytest Docker image and runs this image as a
                    //separate container. The pytest container becomes the agent that Jenkins uses to run the Test
                    //stage of your Pipeline project.
                    image 'qnib/pytest'
                }
            }
        }
            steps {
                //This sh step executes pytest’s py.test command on sources/test_calc.py, which runs a set of
                //unit tests (defined in test_calc.py) on the "calc" library’s add2 function.
                //The --junit-xml test-reports/results.xml option makes py.test generate a JUnit XML report,
                //which is saved to test-reports/results.xml
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
        
           
        
       
    }
}
