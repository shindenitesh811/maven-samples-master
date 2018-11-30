node ("master"){
  stage ("Build") {
    echo "STARTING THE BUILD"
    
    echo 'Checkout source code from GitHub ...'
        retry(5){
            git credentialsId: 'git', url: 'https://github.com/shindenitesh811/maven-samples-master.git'
        }
  } 
}
