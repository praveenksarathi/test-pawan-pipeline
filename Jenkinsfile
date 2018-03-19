def repoPath = 'https://github.com/Plurax/service-time'
def dockerName = 'Test'
def dockerRegistry = '80.158.19.76:5000'
def dockerRepo = 'pawanism'
def dockerImageName = 'test-image-pipeline'

node {
    stage ('Code Pickup'){
        echo 'The Repository path is: ${repoPath}'
        sh 'rm service-time/ -rf'
        echo 'cloning the Repository locally'
        sh "git clone https://github.com/Plurax/service-time "
    }
    stage ('Building the Docker application') {
//        sh "cd service-time/"
        sh "ls"
        echo "Building the application now"
        docker.withRegistry("http://${dockerRegistry}/", 'docker-registry-login') {
        def pcImg
        // Let us tag and push the newly built image.
        echo "BUILD TAG USED FOR IMAGE : ${env.BUILD_NUMBER}";
        pcImg = docker.build("${dockerRepo}/${dockerImageName}:${env.BUILD_NUMBER}", "--network host --file Dockerfile .")
        pcImg.push("${env.BUILD_NUMBER}");
    }
}
}
