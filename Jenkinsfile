node {
    properties([
  	    parameters([
  		    booleanParam(name: 'fromParent', defaultValue: false)
  	    ])
    ])
    
    try {
        stage('Checkout') {
            checkout scm
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
