pipeline {
    agent any
    stages {
        stage('Read Environment Variables from .env file') {
            steps {
                sh 'env'
                script {
                    def envFileContent = readFile('.env')
                    def envMap = [:]

                    envFileContent.split('\n').each { line ->
                        def parts = line.split('=')
                        if (parts.size() == 2) {
                            def key = parts[0].trim()
                            def value = parts[1].trim()
                            envMap[key] = value
                        }
                    }

                    envMap.each { key, value ->
                        env."${key.toUpperCase()}" = value.toString()
                    }
                }
            }
        }
        stage('Use Environment Variables') {
            steps {
                sh 'env'
                withEnv(env) {
                    sh 'echo "My name is $NAME, my age is $AGE, and my occupation is $OCCUPATION"'
                    // Add other steps that use the environment variables here
                }
            }
        }
    }
}
