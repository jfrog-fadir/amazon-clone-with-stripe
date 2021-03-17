node {
    parameters {
        string (name: 'ART_URL', defaultValue: 'http://localhost:8081/artifactory', description: 'Artifactory where artifacts will be deployed/resolved')
        string (name: 'ART_USER', defaultValue: 'admin', description: 'Artifactory user for deploy/resolve artifacts')
        string (name: 'ART_PASSWORD', defaultValue: 'Password1', description: 'Artifactory password for deploy/resolve artifacts')
        booleanParam (name: 'XRAY_SCAN', defaultValue: true, description: 'Scan artifacts using Xray')
        booleanParam (name: 'FAIL_BUILD', defaultValue: true, description: 'Fail build if any violation is found in Xray')
    }

    def server = Artifactory.newServer url: "${params.ART_URL}", username: "${params.ART_USER}", password: "${params.ART_PASSWORD}"
    def rtNpm = Artifactory.newNpmBuild()
    def buildInfo
    
    stage ('Clone') {
        git url: 'https://github.com/jfrog/project-examples.git'
    }



    stage ('Artifactory configuration') {

        rtNpm.deployer repo: 'fadir-npm-local', server: server

        rtNpm.resolver repo: 'fadir-npm-remote', server: server

        rtNpm.tool = 'node6.9.1' // Tool name from Jenkins configuration

        buildInfo = Artifactory.newBuildInfo()

    }



    stage ('Install npm') {

        rtNpm.install buildInfo: buildInfo, path: 'npm-example'

    }



    stage ('Publish npm') {

        rtNpm.publish buildInfo: buildInfo, path: 'npm-example'

    }



    stage ('Publish build info') {

        server.publishBuildInfo buildInfo

    }

}
