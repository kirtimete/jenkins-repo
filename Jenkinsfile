pipeline {
    agent {
        label {
        label "built-in"
        customWorkspace '/data/project'
        }
    }
    stages {
        stage ("clone") {
            steps {
                sh "cd /data/project"
                sh "rm -rf game-of-life"
                sh "git clone https://github.com/kirtimete/game-of-life.git"
            }
        }
        stage ("maven") {
            steps {
			dir ("/data/project/game-of-life") {
              		sh "mvn clean package"		
			
           	 	}
        	}
        }	
	    stage ("deploy") {
		    steps {
			    sh "rm -rf Docker-repository"
			    sh "git clone https://github.com/kirtimete/Docker-repository.git"
			 
			    dir ("/data/project/Docker-repository")
			    
			    {
				    sh "docker-compose up -d" 
			    }
	    }
	    }
   	
    }
}
