pipeline{
    agent any
    // tools { 
    //     maven 'maven' 
    // }
    stages{
        stage("Clean up"){
            steps{
                //  sh '''
                //     echo "PATH = ${PATH}"
                //     echo "M2_HOME = ${M2_HOME}"
                //     mvn -version
                // ''' 
                deleteDir()
            }
        }
        stage("clone repo"){
            steps{
                sh "git clone https://github.com/zhuw726/cicd.git"
            }
        }
        // stage("build"){
        //     steps{
        //         dir("cicd"){
        //             sh "mvn clean install"
        //         }
        //     }
        // }
        // stage("test"){
        //     steps{
        //         dir("cicd"){
        //             sh "mvn test"
        //         }
        //     }
        // }
       stage("build & push docker hub"){
        // environment {
        // HOME = "${env.WORKSPACE}"
        // }
           steps{
            // script {
            //         def dockerHome = tool 'docker'
            //         env.PATH = "${dockerHome}/bin:${env.PATH}"
            // }
               dir("cicd"){
                    // sh " def dockerHome = tool 'docker'"
                    // sh " env.PATH = '${dockerHome}/bin:${env.PATH}'"
                    sh "which docker"
                    // sh "ls -al /var/jenkins_home/tools/org.jenkinsci.plugins.docker.commons.tools.DockerTool/docker/bin/docker"
                    // sh "ls -al /usr/local/bin/docker"
                    sh "cat Dockerfile"
                    sh "ls -al"
                    sh "docker build . -t sample:latest"
                    sh "docker tag sample:latest zhuwj726/tc:latest"
                    sh "docker push zhuwj726/tc:latest"
                }
           }
       }

    }
}
