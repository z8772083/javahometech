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
        DEF Repo =  harbor.tankme.top
        sh """
        docker build -t ${Repo}/dev/${JOB_NAME}:${BUILD_NUMBER} .
        docker login ${Repo} -u admin -p ${Docker_hub}
        docker push ${Repo}/dev/${JOB_NAME}:${BUILD_NUMBER}
        """
    }
   
    stage('Deploy'){
    sh "deploy continue.."
    }
   
}
