pipeline {
	  agent any
	  stages {
	    stage('Build') {
	      steps {
	        script {
	          checkout scm
	          def customImage = docker.build("${registry}:${env.BUILD_ID}")
	        }
	
	      }
	    }
	    stage('unit-test'){
	      steps{
	        script {
	          docker.image("${registry}:${env.BUILD_ID}").inside {c ->
	          sh 'python app_test.py'}
	        
	        }
	      
	      }
	    
	    }
	
	    stage('Publish') {
	      steps {
	        script {
	          docker.withRegistry('', 'dockerhub-id') {
	            docker.image("${registry}:${env.BUILD_ID}").push('latest')
	          }
	        }
	
	      }
	    }
	
	  }
  environment {
    registry = 'zakroj/ci_cd_jenkins'
  }
}
