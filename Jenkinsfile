node {
    stage('Checkout') {
        git credentialsId: 'github-login', url: 'https://github.com/LikeCaffeine/20260622_Jenkins.git'
    }
    
    stage('Build') {
        try {
            sh 'npm build'
        } catch (e) {
            error "빌드 실패: ${e}"
        }
    }
    
    stage('Test') {
        def testsPassed = sh(script: 'npm test', returnStatus: true)
        if (testsPassed != 0) {
            error '테스트 실패!'
        }
    }
    
    stage('Deploy') {
        if (env.BRANCH_NAME == 'main') {
            sh 'npm start'
        } else {
            echo 'Main 브랜치가 아니어서 실행 생략'
        }
    }
}