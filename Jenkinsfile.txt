pipeline {
agent any
stages {
stage ('GIT CHECKOUT') {
steps {
echo "starting checking out fronm GIT";
git branch: 'main', url: 'https://github.com/debashish-DebC/Pipeline_Jenkins_WindowsApp_Batch'
}
}

stage ('Build') {
steps {
echo "Build done and success";
bat 'Build.bat'
}
}

stage ('Unit') {
steps {
echo "Unit testing completed";
bat 'Unit.bat'
}
}

stage ('QA') {
steps {
echo "Quality check done"
bat 'Quality.bat'
}
}

stage ('Deploy') {
steps {
echo "deployment success"
bat 'Deploy.bat'
}
}
}

post {
always {
echo "always run";
}
success {
echo "only success cases";
}
failure {
echo "only for failed";
}
changed {
echo "if any state of pipeline has changed from previous run";
}
}
}
 