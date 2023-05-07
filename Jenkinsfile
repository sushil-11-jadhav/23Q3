pipeline {
	agent {
		label {
			label "built-in"
			customWorkspace "/mnt/http"
		}
	}
	stages {
		stage ("install-docker") {
			steps {
				sh "yum install docker -y"
				sh "service docker start"
			}
		}
		stage ("httpd-container-run") {
			steps {
				sh "rm -rf /mnt/http/*"
				sh "docker run -dp 80:80 --name server httpd"
				sh "git clone https://github.com/sushil-11-jadhav/23Q1.git"
				sh "chmod -R 777 /mnt/http/23Q1/index.html"
				sh "docker cp /mnt/http/23Q1/index.html server:/usr/local/apache2/htdocs"
			}
		}
		stage ("install-docker on slave") {
			agent {
				label {
					label "slave"
					customWorkspace "/mnt/jnlp"
				}
			}
			steps {
				sh "yum install docker -y"
				sh "service docker start"
				sh "rm -rf /mnt/jnlp/*"
				sh "docker run -dp 90:80 --name server httpd"
				sh "git clone https://github.com/sushil-11-jadhav/23Q2.git"
				sh "chmod -R 777 /mnt/jnlp/23Q2/index.html"
				sh "docker cp /mnt/jnlp/23Q2/index.html server:/usr/local/apache2/htdocs"
			}
		}
		stage ("install-docker on slave ssh") {
			agent {
				label {
					label "slave ssh"
					customWorkspace "/mnt/rock"
				}
			}
			steps {
				sh "sudo yum install docker -y"
				sh "sudo service docker start"
				sh "sudo rm -rf /mnt/rock/*"
				sh "sudo docker run -dp 8081:80 --name server httpd"
				sh "sudo git clone https://github.com/sushil-11-jadhav/23Q3.git"
				sh "sudo chmod -R 777 /mnt/rock/23Q3/index.html"
				sh "sudo docker cp /mnt/rock/23Q3/index.html server:/usr/local/apache2/htdocs"
			}
		}
	}
}
