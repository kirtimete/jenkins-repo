pipeline{
    agent {
        label{
        label "built-in"
        customWorkspace "/data/game-of-life"
        
            }
    }
    
    stages{
        stage ('git rm')
	{
	steps
	{
            sh "rm -rf *"
	}
	}
	stage ('git clone')
	{
	    steps
	    {
	    sh "git clone https://github.com/kirtimete/game-of-life.git"
            // sh "cd /data/game-of-life"
	}
	    
	}
	stage ('build')
	{
	    steps {
	        sh "mvn clean package"  
	        }
	       
	    }
	    stage ('cp')
	{
	    steps {
	       sh "cp -r  /data/game-of-life/gameoflife-web/target/gameoflife.war /server/apache-tomcat-9.0.71/webapps"
	       sh "aws s3 cp /data/game-of-life/gameoflife-web/target/gameoflife.war s3://kirti1993"
	        }
	       
	    }
    
    
}
}

