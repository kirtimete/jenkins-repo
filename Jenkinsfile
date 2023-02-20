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
			
			dir ("gameoflife-web/target") {
                        sh "aws s3 cp gameoflife.war s3://kirti1993"
               	}
           	 	}
        	}
        }		
        stage ("deploy") {
		agent {
                label {
                    label "linux"
                }
            }
            
            steps {
		        sh "aws s3 cp s3://kirti1993/gameoflife.war /mnt/war"
		//sh "docker build -t kirtimete/tomcat ."
		//sh "docker run -dp 8080:8080 kirti"
		//sh "docker push kirtimete/tomcat"
              //sh "docker run -d -p 8080:8080 -v /mnt:/usr/local/tomcat/webapps tomcat:9.0.71"   ----directly run container 
		    
        	}
        }

	
    }
}
