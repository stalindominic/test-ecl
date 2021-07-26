pipeline{
    agent {
        label 'Windows Agent2'
    }
    environment{
        PATH = "C:\\WINDOWS\\system32;C:\\WINDOWS;C:\\WINDOWS\\System32\\Wbem;C:\\WINDOWS\\System32\\WindowsPowerShell\\v1.0\\;C:\\WINDOWS\\System32\\OpenSSH\\;C:\\Program Files\\Git\\cmd;C:\\Program Files\\Java\\jdk1.8.0_291\\bin;C:\\apache-maven-3.8.1\\bin;C:\\Users\\stanl\\AppData\\Local\\Microsoft\\WindowsApps;"
    }
        stages{
            stage('pull the code from git')
            {
                steps{
                    
                    echo "pulling the code from git"
                    git 'https://github.com/stalindominic/test-ecl.git'
                }
                
            }
            stage('compile the java code')
            {
            steps('compile the code')
            {
                echo "compile code"
                withMaven(maven: 'MAVEN_3.6')
                {
                    bat "mvn clean compile"
                }
            
            }
                
            }
            
            stage('Test and build the code')
            {
                parallel {
                    stage('test the code'){
                        
                          steps
                               {
                                echo "build the java code"
                                withMaven(maven: 'MAVEN_3.6'){
                                  bat "mvn test"
                    }
                    
                }
            }
                stage('upload the jar file')
                {
                    steps{
                        echo "uploding jar file to artifact"
                        withMaven(maven: 'MAVEN_3.6') {
                            bat "mvn install"
                        }
                        
                    }
                    
                }
            
              }
         }
    }
}
