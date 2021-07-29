pipeline{
    agent any
    environment{
      PATH = "/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin:/usr/share/maven/bin/:/usr/lib/jvm/java-1.8.0/bin"
             //PATH = "C:\\WINDOWS\\system32;C:\\WINDOWS;C:\\WINDOWS\\System32\\Wbem;C:\\WINDOWS\\System32\\WindowsPowerShell\\v1.0\\;C:\\WINDOWS\\System32\\OpenSSH\\;C:\\Program Files\\Git\\cmd;C:\\Program Files\\Java\\jdk1.8.0_291\\bin;C:\\apache-maven-3.8.1\\bin;C:\\Users\\stanl\\AppData\\Local\\Microsoft\\WindowsApps;"
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
                //echo "version of the pipeline: ${params.VERSION1}"
                echo "compile code"
                withMaven(maven: 'MAVEN_3.0')
                {
                    //bat "mvn clean compile"
                    sh "mvn clean compile"
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
                                withMaven(maven: 'MAVEN_3.0'){
                                  //bat "mvn test"
                                    sh "mvn test"
                    }
                    
                }
            }
                stage('upload the jar file')
                {
                    steps{
                        echo "uploding jar file to artifact"
                        withMaven(maven: 'MAVEN_3.0') {
                            //bat "mvn install"
                            sh  "mvn install"
                        }
                        
                    }
                    
                }
            
              }
         }
    }
}
