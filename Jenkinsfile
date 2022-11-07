pipeline {
  agent {label 'windows'}
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {



        stage('Hello2') {
            steps {
                echo 'Hello 2 start'
                bat '''
                cd
                cd tutorials
                ..\\premake5\\win\\premake5.exe vs2022
                "C:\\Program Files\\Microsoft Visual Studio\\2022\\Professional\\Msbuild\\Current\\Bin\\amd64\\MSBuild.exe" Tutorials.sln /p:Configuration=release /p:Platform="x64" /m
                '''
                echo 'Hello 2 end'
            }
        }
        
        
        
         stage('Hello3') {
      //      agent {
      //          label 'windows'
      //      }
            steps {
                echo 'Hello 3 start'
                bat '''
                cd
                cd tutorials/Bin
                05_basic_scene64.exe
                '''
                echo 'Hello 3 end'
            }
        }



  }
  post {
    always {
        junit(
          allowEmptyResults: true, 
          testResults: '**/build/test-results/test/*.xml'
        )
    }
  }
}
