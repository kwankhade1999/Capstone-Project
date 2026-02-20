pipeline {
    agent any
    environment {
        SONAR_HOME = tool "Sonar"
    }
    parameters {
        choice(
            name: 'DEPLOY_ENV',
            choices: ['dev', 'prod'],
            description: 'Choose the environment to deploy: DEV or PROD'
        )
    }

    stages {

        stage("Code Checkout") {
            steps {
                git(
                    url: "https://github.com/DevOps-Playbook/Capstone-Project.git",
                    branch: "main",
                    credentialsId: "jenkins-git",
                    changelog: true,
                    poll: true
                )
            }
        }

        stage("Docker Build, Tag, and Push") {
            steps {
                script {
                    def condition = false

                    if (condition) {
                        def dockerImage = "amigo-nishant/dify"
                        def dockerTag = "latest"

                        withCredentials([usernamePassword(credentialsId: 'dockerhub-cred-id')]) {
                            sh "docker build -t ${dockerImage}:${dockerTag} ."
                            sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER -p"
                            sh "docker push ${dockerImage}:${dockerTag}"
                        }
                    } else {
                        if (fileExists('docker')) {
                            sh 'cd docker'
                        } else {
                            error "Docker doesn't exist"
                        }
                    }
                }
            }
        }

        stage("SonarQube Code Analysis") {
            steps {
                withSonarQubeEnv("Sonar") {
                    sh """
                    $SONAR_HOME/bin/sonar-scanner \
                    -Dsonar.projectName=dify \
                    -Dsonar.projectKey=dify \
                    -Dsonar.sources=. \
                    -Dsonar.exclusions=**/node_modules/**,**/*.test.js,**/vendor/**,**/*.md
                    """
                }
            }
        }

        stage("Trivy File System Scan") {
            steps {
                sh "trivy fs --format table -o trivy-fs-report.html ."
            }
        }

        stage("OWASP Dependency Check") {
            steps {
                echo "Skipping due to some dependency test cases are yet to be merged to master"
                // dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'dc'
                // dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

        stage('Setup Namespaces') {
            steps {
                script {
                    echo "Ensuring namespaces 'dev' and 'prod' exist..."

                    def namespace = ['dev', 'prod']

                    namespace.each { ns ->
                        echo "Checking if namespace '${ns}' exists..."
                        def nsExists = sh(script: "kubectl get namespace ${ns} --ignore-not-found=true", returnStatus: true) == 0

                        if (nsExists) {
                            echo "Namespace '${ns}' already exists. Skipping creation."
                        } else {
                            echo "Namespace '${ns}' does not exist. Creating..."
                            sh "kubectl create namespace ${ns}"
                        }
                    }
                }
            }
        }

        stage('Verify Namespaces before deployment') {
            steps {
                script {
                    echo "Listing all namespaces"
                    sh "kubectl get ns"
                }
            }
        }

        stage("Deployment Stage") {
            steps {
                script {
                    def namespace = params.DEPLOY_ENV
                    echo "Deploying to namespace: ${namespace}"

                    def helmPath = 'Helm/charts/dify'
                    def releaseName = 'dify'

                    def releaseExists = sh(script: "helm status ${releaseName} -n ${namespace}", returnStatus: true) == 0

                    if (releaseExists) {
                        sh "helm upgrade --install ${releaseName} ${helmPath} -n ${namespace}"
                    } else {
                        sh "helm repo add dify https://borispolonsky.github.io/dify-helm"
                        sh "helm repo update"
                        sh "helm upgrade --install release dify/dify -n ${namespace} --dry-run --debug"
                        sh "helm upgrade --install release dify/dify -n ${namespace}"
                    }
                }
            }
        }

    }
}
