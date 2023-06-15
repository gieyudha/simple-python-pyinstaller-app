node {
    stage('Build') {
        docker.image('python:2-alpine').withRun('-p 3007:3007') {
        sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    stage('Test') {
        docker.image('qnib/pytest').withRun('-p 3007:3007') {
        sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        post {
            always {
                junit 'test-reports/results.xml'
            }
        }
        }
    }
}