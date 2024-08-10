pipeline{
    agent any
    tools{
        jdk "jdk11"
        maven "maven3"
    }
    stages{
        stage("Scan SonarQube"){
            steps{
                sh "mvn clean package"
                sh ''' mvn sonar:sonar -Dsonar.url=https://http://localhost:9000 -Dsonar.login=squ_12d7c8f50a9c9a188b980c224f1117edd80373da \
                -Dsonar.projectName=Spring \
                -Dsonar.projectKey=Spring \
                -Dsonar.java.binaries=. '''
            }
        }

        stage("Unit Test") {
            steps{
                sh "./mvnw test"
                //Execute the test
            }

            post{
                always{
                    junit '**/target/surefire-reports/TEST-**.xml'
                    //Display reports
                }
            }
        }
    }
}