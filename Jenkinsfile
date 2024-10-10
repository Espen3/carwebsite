node('ubuntu-Appserver-1')
{

def app
stage('Cloning Git')
{
    /* Let's make sure we have the repository cloned to our workspace */
    checkout scm
}

stage('Build-and-Tag')
{
    /* This builds the actual image; 
         * This is synonymous to docker build on the command line */
    app = docker.build('Espen3/car_docker_repo')
}

stage('Post-to-dockerhub')
{
    docker.withRegistry('https://registry.hub.docker.com', 'docker_prop')
    {
        app.push('latest')
    }
   
}

stage('Deploy')
{
    sh "docker-compose down"
    sh "docker-compose up -d"
}

}





