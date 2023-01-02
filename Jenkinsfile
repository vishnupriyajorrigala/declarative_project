pipeline {

  agent any

  stages {

         stage('Maven Compile'){

         steps{

               echo 'Project compile stage'

               bat label: 'Compilation running', script: '''mvn compile'''

             }

         }

 

          stage('Unit Test') {

          steps {

              echo 'Project Testing stage'

              bat label: 'Test running', script: '''mvn test'''

       

               }

         }

        stage('Jacoco Coverage Report') {

        steps{

            jacoco()

         }

       }
       stage('SonarQube'){

       steps{

             bat label:'',script:'''mvn sonar:sonar\

             -Dsonar.host.url=http://localhost:9000\

              -Dsonar.login=squ_4f0cb92cd9347324a7ca98ec0baf84b1edc5aec0'''

             }

         } 
 

         stage('Maven Package'){

           steps{

                echo 'Project packaging stage'

                bat label: 'Project packaging', script: '''mvn package'''

                }

            } 
        stage('Generate Cucumber report') {
            steps{
                 cucumber buildStatus: 'UNSTABLE',
                      reportTitle: 'My Cucumber Report',
                      fileIncludePattern: '**/*.json',
                         trendsLimit: 10,
                      classifications: [
                          [
                              'key': 'Browser',
                              'value': 'Chrome'
                          ]
                      ]
                  }
         }
         
          

  }
  
}
