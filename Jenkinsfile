node('ubuntu-Appserver-1')
{

def app
stage('Cloning Git')
{
    /* check to make sure we have the repo */
    checkout scm
}

stage('Build-and-Tag')
{
    /* building the image */
    app = docker.build('eapen303/car_docker_repo')
}

stage('Post-to-dockerhub')
{
    /* pushing to dockerhub using the right creds - might need an app = */
    docker.withRegistery('https://registry.hub.docker.com', 'docker_prop')
    {
        app.push('latest')
    }
}

stage('Deploy')
{
    /* deploy */
    sh "docker-compose down"
    sh "docker-compose up -d"
}

}