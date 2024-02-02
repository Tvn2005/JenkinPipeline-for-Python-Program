This is a sample program to build for a python program in Jenkins.It has following steps:
1.Created a sample python program in a repository.
2.In Jenkins, using pipeline item and configuring it.No Triggers were added.Just a pipeline script was added as follows:
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Jenkins-example-github', url: 'https://github.com/Tvn2005/JenkinPipeline-for-Python-Program.git']])
            }
        }
        stage("Build"){
            steps {
                git branch: 'main', credentialsId: 'Jenkins-example-github', url: 'https://github.com/Tvn2005/JenkinPipeline-for-Python-Program.git'
                bat 'python List_prg.py'
            }
        }
        stage('Test'){
            steps{
                echo "Job has been tested"
            }
        }

There are multiple stages can be added however, three stages have been used here i.e. Checkout,Buld and Test.The steps can be genarated using pipeline scripts.
3. For GitHub and Jenkins integration, generate a access token from developer setttings(Tick repos,user:email and read:org) in Github profile settings.In Jenkins, choose username and password under add credentials and paste token in place of password and write username as your Github.
4.Apply and Save the changes and Test the program.
