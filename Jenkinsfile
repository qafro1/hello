podTemplate(yaml: '''
    apiVersion: v1
    kind: Pod
    metadata:
      labels: 
        some-label: some-label-value
    spec:
      containers:
      - name: python
        image: python:latest
        command:
        - sleep
        args:
        - 99d
    ''') {
    node(POD_LABEL) {
      container('python') {
        echo POD_CONTAINER // displays 'busybox'
        sh 'pip install -r requirements.txt'
        sh 'python helloworld.py'
      }
    }
}