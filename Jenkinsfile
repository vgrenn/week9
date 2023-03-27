podTemplate(yaml: '''
    apiVersion: v1
    kind: Pod
    spec:
      containers:
      - name: centos
        image: centos
        command:
        - sleep
        args:
        - 99d
    restartPolicy: Never
 ''') {
 node(POD_LABEL) {
 stage('k8s') {
 git branch:'main', url:'https://github.com/vgrenn/week9.git'
 container('centos') {
 stage('start calculator') {
 sh '''
 pwd
 cd Chapter09/sample3
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
 chmod +x ./kubectl
 ./kubectl version --client
 pwd
 ./kubectl apply -f calculator.yaml -n staging
 ./kubectl apply -f hazelcast.yaml -n staging
 sleep 30
 ./kubectl get pods -n staging
 ./kubectl delete deployments calculator-deployment -n staging
 ./kubectl delete deployments hazelcast -n staging
 '''
 }
 }
 }
 }
 }
