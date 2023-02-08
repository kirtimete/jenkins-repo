pipeline{
    agent {
        label{
        label "built-in"
        customWorkspace "/data"
        
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
            sh "cd /data/game-of-life"
	}
	    
	}
	stage ('build')
	{
	    steps {
	        sh "mvn -f /data/game-of-life/pom.xml install"  
	        }
	       
	    }
	    stage ('cp')
	{
	    steps {
	       sh "cp -r  /data/game-of-life/gameoflife-web/target/gameoflife.war /server/apache-tomcat-9.0.71/webapps"
	       sh "aws s3 cp /data/game-of-life/gameoflife-web/target/gameoflife.war s3://kirti1993"
	        }
	       
	    }
    
    
    stage ('stage-slave') 
    {
        agent
        {
        node {
            label 'linux-slave-1'
            customWorkspace "/home/ec2-user"
        } 
        
        }
        steps('deploy')
        {
            dir ('/data/gameoflife'){
	         sh "aws s3 cp s3://kirti1993/gameoflife.war /server/apache-tomcat-9.0.71/webapps/ --recursive"
            }
        }
    }
}
}

