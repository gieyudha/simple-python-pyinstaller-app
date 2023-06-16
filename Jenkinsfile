node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    stage('Test') {
        docker.image('qnib/pytest').inside {
            try {
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            } catch (e) {
                throw e
            } finally {
                junit 'test-reports/results.xml'
            }
        }
    }
    stage('Deploy') {
        boolean result = true
        docker.image('cdrx/pyinstaller-linux:python2').inside {
            try {
                sh 'pyinstaller --onefile sources/add2vals.py'
            } catch (e) {
                result = false
            } 

            if(result == true){
                archiveArtifacts 'dist/add2vals'
            }
        }
    }
}