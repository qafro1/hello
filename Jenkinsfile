podTemplate(yaml: '''
spec:
  containers:
  - name: python
    image: python:latest
    command:
    - sleep
    - 99d
  terminationGracePeriodSeconds: 3
''') {
  retry(count: 2, conditions: [kubernetesAgent()]) {
    node(POD_LABEL) {
        container('python') {
            sh 'pip install -r requirements.txt'
            sh 'python helloworld.py'
        }
    }
  }
}