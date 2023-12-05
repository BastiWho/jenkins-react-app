node {
  stage('Checkout') {
    // Use the Git plugin to checkout the code
    git branch: 'master', url: 'https://github.com/BastiWho/jenkins-react-app.git'
  }
  stage('Build') {
    sh 'docker ps --filter name=node | grep node && docker kill node || true'
    sh 'docker run -d --rm --name node -v ${WORKSPACE}:/var/app -w /var/app node:lts-bullseye tail -f /dev/null'
    sh 'docker exec node npm --version'
    sh 'docker exec node ls -la'
    sh 'docker exec node npm ci'
    sh 'docker exec node npm install -g npm@10.2.4'
    sh 'docker exec node npm run build'
    sh 'docker kill node'
  }
  stage('Cleanup') {
    // Use the Git plugin to checkout the code
    deleteDir()
  }
}
