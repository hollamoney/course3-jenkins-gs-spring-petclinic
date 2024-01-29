echo "Fenerbahce şampiyon"
node {
    stage('checkout'){
    powershell 'dir'
    git branch: 'main', url:'https://github.com/hollamoney/course3-jenkins-gs-spring-petclinic.git'
    }
    stage('build'){
        powershell 'mvn clean install'
    }
    parallel testsA :{
        powershell "echo test set A"
        sleep 2
        sleep 3
    },testB: {
        powershell "echo test set B"
        sleep 4
    },testC:{
        sleep 1
        powershell "echo test set C"
    }
    stage('test') {
        powershell 'mvn test'
    }
    stage('capture'){
        archiveArtifacts  '**/target/*.jar'
        jacoco()
        junit '**/target/surefire-reports/TEST*.xml'
    }
    emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
    subject: "${currentBuild.currentResult} : Job ${env.JOB_NAME} to: 'mehmet@kartalci.com'"
}
