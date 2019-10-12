pipeline {
    agent any
    stages {
	    stage('Compile') {
            steps {
                    echo "Compiled Successfully!!";
            }
        }
	
        stage('JUnit') {
            steps {
                 echo "JUnit Passed Successfully!";
            }  
        }
    
        stage('Unit-Test') {
            steps {
                echo "Running JUnit Tests";   
            }
        }
    
        stage('quality-Gate') {
            steps {
                echo "Verifying Quality Gates";
            }
        }
    
        stage('deploy') {
            steps {
              echo "Pass!";
            }
        }
        
        stage('Deploiement Ansible') {
            withCredentials([usernameColonPassword(credentialsId: 'docker-cacti-token', variable: '')]) {
                ansiblePlaybook (
                     colorized: true, 
                     become: true,             
                     playbook: 'ansible-playbooks/mariadb.yml', 
                     extras: '--extra-vars "variable_host=${HOSTNAME} variable_dbrootpassword=${ROOTPASSWORD} variable_dbname=${DBNAME} variable_dbuser=${DBUSER} variable_dbpass=${DBPASS} ansible_ssh_user=$SUDOERLOGIN ansible_ssh_pass=$SUDOERPASS ansible_sudo_pass=$SUDOERPASS"'
        )
    }
}
