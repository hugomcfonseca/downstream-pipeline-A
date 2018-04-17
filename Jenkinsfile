node {
    properties([
  	    parameters([
  		    booleanParam(name: 'fromParent', defaultValue: false)
  	    ])
    ])
    
    env.AFRAMZ_BUILD_ID = env.BUILD_ID
    env.JOB_NAME = env.BRANCH_NAME
    
    try {
        stage('Checkout') {
            checkout scm
        }
        
        stage('List env variables') {
            sh 'printenv'   
        }

        stage('List workspace') {
            sh 'ls -laht ${WORKSPACE}'
        }
    } catch (err) {
        print(err.getMessage())
        currentBuild.result = 'FAILURE'
    } finally {
        step([
            $class: 'WsCleanup',
            deleteDirs: true,
            patterns: [
                [
                    pattern: '.git/**', type: 'EXCLUDE'
                ]
            ]
        ])
    }
}
