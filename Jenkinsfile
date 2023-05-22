pipeline {
  environment {
    //
    // you need a credential named 'docker-hub' with your DockerID/password to push images
    CREDENTIAL = "docker-hub"
    DOCKER_HUB = credentials("$CREDENTIAL")
    REGISTRY = "docker.io"
    REPOSITORY = "${DOCKER_HUB_USR}/${JOB_BASE_NAME}"
    BRANCH_NAME = "${GIT_BRANCH.split("/")[1]}"
    TAG = "${BRANCH_NAME}"
    IMAGELINE = "${REGISTRY}/${REPOSITORY}:${TAG} Dockerfile"
    //
  } // end environment 
  
  agent any
  
  stages {
    
    stage('Checkout SCM') {
      steps {
        checkout scm
      } // end steps
    } // end stage "checkout scm"
    
    stage('Build and Push Image') {
      steps {
        sh """
          echo ${DOCKER_HUB_PSW} | docker login -u ${DOCKER_HUB_USR} --password-stdin
          docker build -t ${REPOSITORY}:${TAG} --pull -f ./Dockerfile .
          docker push ${REPOSITORY}:${TAG}
        """
      } // end steps
    } // end stage "build and push"
    
    stage('Analyze Image with Anchore plugin') {
      steps {
        // anchore plugin for jenkins: https://www.jenkins.io/doc/pipeline/steps/anchore-container-scanner/
        // first, we need to write out the "anchore_images" file which is what the plugin reads to know
        // which images to scan:
        writeFile file: 'anchore_images', text: IMAGELINE
        // call the scanner, wrapin catchError so we can break the pipeline but still run the
        // cleanup stage if the evaluation fails
        catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
          // forceAnalyze is a good idea since we're passing a Dockerfile with the image
          anchore name: 'anchore_images', forceAnalyze: 'true', engineRetries: '900'
        }
        // if we want to use the command line tool anchorectl instead of the jenkins plugin
        // please take a look at https://github.com/pvnovarese/anchorectl-pipeline 
        // and https://github.com/pvnovarese/2023-03-demo/blob/main/Jenkinsfile-anchorectl
        //
        // if you want continuous re-evaluation in the background, you can turn it on with these:
        // sh """
        //   curl -sSfL  https://anchorectl-releases.anchore.io/anchorectl/install.sh  | sh -s -- -b $HOME/.local/bin  
        //   export PATH="$HOME/.local/bin/:$PATH"   
        //   anchorectl subscription activate policy_eval ${IMAGE}
        //   anchorectl subscription activate vuln_update ${IMAGE}
        // """
        // and in this case you would probably also want to configure "policy & vulnerability" updates
        // in "Events & Notifications" -> "Manage Notification Endpoints" 
        //
      } // end steps
    } // end stage "analyze image 1 with anchore plugin"     
    
    // optional, you could promote the image here 
    // 
    // stage('Promote Image') {
    //  steps {
    //    sh """
    //      docker tag ${REPOSITORY}:${TAG} ${REPOSITORY}:${BRANCH_NAME}
    //      docker push ${REPOSITORY}:${BRANCH_NAME}
    //    """
    //  } // end steps
    // } // end stage "Promote Image"        
    
    stage('Clean up') {
      steps {
        //
        // don't need the image(s) anymore so let's rm it
        //
        sh 'docker image rm ${REPOSITORY}:${TAG} ${REPOSITORY}:${BRANCH_NAME} || failure=1'
        // the || failure=1 just allows us to continue even if one or both of the tags we're
        // rm'ing doesn't exist (e.g. if the evaluation failed, we might end up here without 
        // re-tagging the image, so ${BRANCH_NAME} wouldn't exist.
        //
        // if we used anchore-cli above, we should probably use the plugin here to archive the evaluation
        // and generate the report:
        //anchore name: 'anchore_images', forceAnalyze: 'true', engineRetries: '900'        
      } // end steps
    } // end stage "clean up"
    
  } // end stages
  
} // end pipeline 
