
pipeline {
          agent any
          stages{
            stage('Checkout GIT'){
                steps{
                    echo 'Pulling...';
                    git branch: 'main',
                    url : 'https://github.com/Hadj-Sessi-Heni/CI.git';
                }

            }
            stage('MVN CLEAN'){
            steps{
                echo 'Pulling...';
                sh 'mvn clean'
                }
            }
             stage('MVN COMPILE'){
                steps{
                sh 'mvn compile'
                }
             }
             stage('MVN PACKAGE'){
                steps{
                sh 'mvn package'
                }
             }
             stage('MVN TEST'){
                steps{
                 sh 'mvn test'
                 }
             }

              stage('MVN SONARQUBE '){
                 steps{
                    sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=esprit'
                 }
              }
              stage("nexus deploy"){
                 steps{
                  //nexusArtifactUploader artifacts: [[artifactId: 'ExamThourayaS2', classifier: '', file: '/var/lib/jenkins/workspace/projetci/target/ExamThourayaS2-0.0.1-SNAPSHOT.jar', type: 'jar']], credentialsId: 'nexus-snapshots', groupId: 'tn.esprit', nexusUrl: '192.168.95.158:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'nexus-snapshots', version: '2.2.4'
                  nexusArtifactUploader artifacts: [[artifactId: 'ExamThourayaS2', classifier: '', file: '/var/lib/jenkins/workspace/projetci/target/ExamThourayaS2-0.0.1-SNAPSHOT.jar', type: 'jar']], credentialsId: 'nexus-snapshots', groupId: 'tn.esprit', nexusUrl: '192.168.95.158:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'nexus-snapshots', version: '0.0.1-SNAPSHOT'
                 }
              }
              stage('Build Docker Image') {
                 steps {
                 sh 'docker build -t henihs98/springci:1.0.0 .'
                 }
              }
              stage('Push Docker Image') {
                   steps {
                     sh "docker login -u henihs98 -p 203JMT1661"
                     }
                     sh 'docker push henihs98/springci:1.0.0'
                   }
              }
              stage('DOCKER COMPOSE') {
                   steps {
                      sh 'docker-compose up -d --build'
                   }
              }
              }
          }








