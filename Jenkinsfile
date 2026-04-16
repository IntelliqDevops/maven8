pipeline
{
    agent any
    stages
    {
        stage('Download')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage('Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'e84c4b79-ad8f-4a55-a74b-7771418a216c', path: '', url: 'http://172.31.28.179:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('Testing')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
                
            }
        }
        stage('Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'e84c4b79-ad8f-4a55-a74b-7771418a216c', path: '', url: 'http://172.31.31.200:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
    }
}
