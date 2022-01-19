node('master') 
{
    stage('ContinuousDownload')
    {
        git 'https://github.com/intelliqittrainings/maven.git'             
    }
    stage('ContinuousBuild')
    {
        sh 'mvn package'
    }
    stage('ContinuousDeployment')
    {
        deploy adapters: [tomcat9(credentialsId: 'fb0e5724-bffc-4899-8c17-7b98bb63e6e5', path: '', url: 'http://172.31.26.47:8080')], contextPath: 'testapp', war: '**/*.war'
    }
    stage('ContinuousTesting')
    {
         git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
         sh 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar'
    }
    stage('ContinuousDelivery')
    {
        deploy adapters: [tomcat9(credentialsId: 'fb0e5724-bffc-4899-8c17-7b98bb63e6e5', path: '', url: 'http://172.31.26.47:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
}
