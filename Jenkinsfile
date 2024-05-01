pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP_REPO = 'cicd-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = '4849@Nexus'
        RELEASE_REPO = 'cicd-release'
        CENTRAL_REPO = 'cicd-maven-central'
        NEXUSIP = '172.31.49.77'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'cicd-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage ('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage ('Test'){
            steps {
                sh 'mvn test'
            }

        }

        satge ('Checkstyle Analysis'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }       
    }
}