#이미지 빌드시 이름을 ECR 쪽으로 변경
app = docker.build("129598177799.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins-ploonet-test")

# ECR에서 생성한 Repository URI로 변경 및 Jenkins AWS Credential으로 변경
docker.withRegistry('https://129598177799.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins-ploonet-test', 'ecr:ap-northeast-2:jenkins-aws-ploonet-credentials')

# Full Code
  
node {
     stage('Clone repository') {
         checkout scm
     }

     stage('Build image') {
         app = docker.build("129598177799.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins-ploonet-test")
     }

     stage('Push image') {
         sh 'rm  ~/.dockercfg || true'
         sh 'rm ~/.docker/config.json || true'
         
         docker.withRegistry('https://129598177799.dkr.ecr.ap-northeast-2.amazonaws.com/jenkins-ploonet-test', 'ecr:ap-northeast-2:jenkins-aws-ploonet-credentials') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
     }
  }
}
