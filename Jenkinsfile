pipeline {
    agent any
    tools {
        
         maven "MAVENHOME"
    }
    environment {
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus2"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "localhost:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "myRepository"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "NEXUSCRED"
    }
    stages {
        
         stage('Initialize'){
            steps{
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }
        
        stage("clone code") {
            steps {
                script {
                    // Let's clone the source
                  //  git 'https://github.com/SreedeviPK/mydemo.git';
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SreedeviPK/mydemo.git']]])
                }
            }
        }
        stage("mvn build") {
            steps {
                script {
                    // If you are using Windows then you should use "bat" step
                    // Since unit testing is out of the scope we skip them
                 
                   // bat(/${MAVENHOME}\bin\mvn -Dmaven.test.failure.ignore clean package/)
                      bat(/${MAVENHOME}\bin\mvn clean install/)
                }
            }
        }
       /* stage("publish to nexus") {
            steps {
                script {
                   // Read POM xml file using 'readMavenPom' step , this step 'readMavenPom' is included in: https://plugins.jenkins.io/pipeline-utility-steps
                    pom = readMavenPom file: "pom.xml";
                    // Find built artifact under target folder
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    // Print some info from the artifact found
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    // Extract the path from the File found
                    artifactPath = filesByGlob[0].path;
                    // Assign to a boolean response verifying If the artifact name exists
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: '${BUILD_NUMBER}',
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                // Artifact generated such as .jar, .ear and .war files.
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                // Lets upload the pom.xml file for additional information for Transitive dependencies
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                        mvn '''deploy:deploy-file -DgeneratePom=false -DrepositoryId=myRepository -Durl=http://localhost:8081/nexus/content/repositories/myRepository -DpomFile=C:/Users/sreedevi.k03/.jenkins/workspace/mydemo/pom.xml -Dfile=C:/Users/sreedevi.k03/.jenkins/workspace/mydemo/target/spring3-mvc-maven-xml-hello-world-1.2.war'''
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                      //  mvn '''deploy:deploy-file -DgeneratePom=false -DrepositoryId=myRepository -Durl=http://localhost:8081/nexus/content/repositories/myRepository -DpomFile=C:/Users/sreedevi.k03/.jenkins/workspace/mydemo/pom.xml -Dfile=C:/Users/sreedevi.k03/.jenkins/workspace/mydemo/target/spring3-mvc-maven-xml-hello-world-1.2.war'''

                }
            }
        }*/
         stage("nexus"){
            steps{
                script{
                    echo "published"
                   // pom = readMavenPom file: "pom.xml";
                   //  artifactPath = filesByGlob[0].path;
                   // mvn deploy:deploy-file -DgeneratePom=false -DrepositoryId=myRepository -Durl=NEXUS_URL -DpomFile=pom -Dfile= artifactPath
                }
            }
        } 
        
        stage("deploy"){
            steps{
                script{
                  // //bat '''curl http://localhost:8081/nexus/content/repositories/myRepository/com/madhu/spring3-mvc-maven-xml-hello-world/1.2/spring3-mvc-maven-xml-hello-world-1.2.war -o C:\\Program Files\\Apache Software Foundation\\Tomcat 9.0\\webapps'''
                 
                    echo "deploy stage"
                }
            }
        } 
        
    }
}
