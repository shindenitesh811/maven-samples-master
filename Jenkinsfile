node ("master"){
  
  def mvnHome = tool name: 'maven-3', type: 'maven'
  
  env.BN = VersionNumber([
        versionNumberString : '${BUILD_MONTH}.${BUILDS_TODAY}.${BUILD_NUMBER}', 
        projectStartDate : '2018-11-30', 
        versionPrefix : 'v1.'
    ])
  
  stage ("CHECKOUT THE SCM") {
    echo 'Checkout source code from GitHub ...'
        retry(5){
            git credentialsId: 'git', url: 'https://github.com/shindenitesh811/maven-samples-master.git'
        }
  }
  
 
  stage("MVN change version and package"){
    sh "${mvnHome}/bin/mvn versions:set -DnewVersion=$BN -DgenerateBackupPoms=false"
    sh "${mvnHome}/bin/mvn clean package"
    sh "${W_GIT_HOME} checkout -b release_${BN}"  
        
  }
  
   stage("Build Docker Image"){
    sh "cd /etc/user/"
    sh "docker build -t shindenitesh811/maven-samples-master ."
  }
  
  stage ("STASHING THE CODE"){
    echo 'Stash the project source code ...'
        stash includes: '**', name: 'SOURCE_CODE'
  }
  
  
}
