node{
   
    stage('Git Clone From Github'){
        git branch: 'dev', url: 'https://github.com/z8772083/javahometech.git'
    }
   
    stage('Maven Build'){
        def MvnHome = tool name: 'maven', type: 'maven'
        def MvnCmd = "${MvnHome}bin/mvn"
        sh "${MvnCmd} -Dskiptest clean package"
    }

    stage('Build and Push image'){
        sh """
        docker build -t harbor.tankme.top/dev/javahometech:01 .
        docker login harbor.tankme.top -u admin -p ${Docker_hub}
        docker push harbor.tankme.top/dev/javahometech:01
        """
    }
   
    stage('Deploy'){
    sh 'deploy continue..'
    }
   
}
