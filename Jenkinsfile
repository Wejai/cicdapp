node {
    dir("/var/jenkins_home/workspace/"){
    checkout scm

    env.DOCKER_API_VERSION="1.38"
    appName = "bankdemo/cicd-app"
    registryHost = "mycluster.icp:8500/"
    imageName = "${registryHost}${appName}:latest"
    env.BUILDIMG=imageName
    docker.withRegistry('https://mycluster.icp:8500/', 'docker'){
    stage "Build"

        def pcImg = docker.build("mycluster.icp:8500/bankdemo/cicdapp:latest", "-f Dockerfile.ppc64le .")
       
        pcImg.push()

    input 'Do you want to proceed with Deployment?'
    stage "Deploy"

        sh "kubectl set image deployment/demoapp-demochart demochart=${imageName}"
        sh "kubectl rollout status deployment/demoapp-demochart"
}
}
}

