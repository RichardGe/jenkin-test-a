pipeline {


  // agent {label 'windows'}
  agent none


  // options {
  //   buildDiscarder(logRotator(numToKeepStr: '5'))
  // }


	stages {


		stage('Hello0') {
			agent {
				label 'linux'
			}
			steps {
				echo 'Hello0 start'
				echo 'Hello0 end'
			}
		}



		stage('Build_Linux') {

			agent {
				label 'linux'
			}

			steps {
				echo 'Build_Linux start'
				sh '''
				echo "hello world for Build_Linux"
				pwd
				cd tutorials
				chmod +x ../premake5/linux64/premake5
				../premake5/linux64/premake5 gmake
				make -j config=release_x64
				dir
				'''
				echo 'Build_Linux end'
			}
		}




		stage('Build_Windows') {

			agent {
				label 'windows'
			}

			steps {
				echo 'Build_Windows start'
				bat '''
				cd
				cd tutorials
				..\\premake5\\win\\premake5.exe vs2022
				"C:\\Program Files\\Microsoft Visual Studio\\2022\\Professional\\Msbuild\\Current\\Bin\\amd64\\MSBuild.exe" Tutorials.sln /p:Configuration=release /p:Platform="x64" /m
				cd Bin
				dir
				'''
				echo 'Build_Windows end'
			}
		}
		
		
		
		 stage('Run_Windows') {

			agent {
				label 'windows'
			}

			steps {
				echo 'Run_Windows start'
				bat '''
				cd
				cd tutorials/Bin
				05_basic_scene64.exe
				'''
				echo 'Run_Windows end'
			}
		}



		
		 stage('Run_Linux') {

			agent {
				label 'linux'
			}

			steps {
				echo 'Run_Linux start'
				sh '''
				pwd
				dir
				cd tutorials/Bin
				export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./../../RadeonProRender/binUbuntu18/
				chmod +x ./05_basic_scene64
				./05_basic_scene64
				'''
				echo 'Run_Linux end'
			}
		}





  }


 // post {
 //   always {
  //	  junit(
  //		allowEmptyResults: true, 
   //	   testResults: '**/build/test-results/test/*.xml'
   //	 )
   // }
 // }


	post {
		always {
			echo 'post/always'
		}

		success {
			echo 'post/success'
		}

		failure {
			echo 'post/failure'
		}

		cleanup {
			echo 'post/cleanup'
		//	deleteDir()
		}
	}





}
