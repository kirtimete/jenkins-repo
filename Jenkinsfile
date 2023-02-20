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
			
			//dir ("gameoflife-web/target") {
                        //sh "aws s3 cp gameoflife.war s3://kirti1993"
              // 	}
           	 	}
        	}
        }	
	    stage ("deploy") {
		    steps {
			    sh "rm -rf Docker-repository"
			    sh "git clone https://github.com/kirtimete/Docker-repository.git"
			 
			    sh "cd /data/project/Docker-repository"
			    
	    	  // sh "cp /data/project/game-of-life/gameoflife-web/target/gameoflife.war /mnt/war"
		  // dir ("/mnt"){
		  sh "docker-compose up -d"
		//  }
	    }
	    }
     //   stage ("deploy") {
	//	agent {
          //      label {
            //        label "linux"
              //  }
            // }
            
          //  steps {
		//        sh "aws s3 cp s3://kirti1993/gameoflife.war /mnt/war"
		  //  dir ("/mnt"){
			//    sh "docker-compose up"
		//sh "docker build -t kirtimete/tomcat ."
		//sh "docker run -dp 8080:8080 kirti"
		//sh "docker push kirtimete/tomcat"
              //sh "docker run -d -p 8080:8080 -v /mnt:/usr/local/tomcat/webapps tomcat:9.0.71"   ----directly run container 
		//    }
        	//}
       // }

	
    }
}
