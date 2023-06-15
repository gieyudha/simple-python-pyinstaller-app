node {
    stage('Build') {
        docker.image('python:2-alpine').inside() {
            sh 'python3 -m py_compile ./sources/add2vals.py ./sources/calc.py'
        }
    }
    stage('Test') {
        docker.image('qnib/pytest').inside() {
            sh 'py.test --verbose --junit-xml test-reports/results.xml ./sources/test_calc.py'
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
    }
}