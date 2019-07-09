def label = "waiting-game-${UUID.randomUUID().toString()}"

podTemplate(label: label, 
yaml: """
apiVersion: v1
kind: Pod
metadata:
  namespace: bankdemo 
spec:
  containers:
    - name: ubuntu
      image: ubuntu
      tty: true
"""
) {
     node(label){
       stage('Run'){
         container('ubuntu') {
           echo 'waiting game'
           sleep 5
           echo 'bye'
         }
       }
    }
}