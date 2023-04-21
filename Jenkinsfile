pipeline{

	agent any

		stages{

			stage('Checkout'){

					steps{

						git branch: "main", url: 'https://github.com/RagaVeeraswapna/allergy_microservice.git'

						}

					}

			stage('Build'){

					steps{

						sh 'chmod a+x mvnw'

						sh './mvnw clean package -DskipTests=true'

						}

					post{

						always{

							archiveArtifacts 'target/*.jar'

							}

						}

				}

			stage(DockerBuild) {

						steps {

							sh 'docker build -t veeraswapnaraga/allergy-microservice:latest .'

							}

						}

			stage('Login') {

					steps {

						sh 'echo Veera@441 | docker login -u veeraswapnaraga --password-stdin'

						}

					}

			stage('Push') {

					steps {

						sh 'docker push veeraswapnaraga/allergy-microservice'

						}
	
					}
				}

		post {

			always {

				sh 'docker logout'

				}

			}

}