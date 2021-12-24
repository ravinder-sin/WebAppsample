pipeline { 
    agent any  
    stages { 
        stage('Build') { 
            steps { 
               sh 'mvn install package' 
            }
        }
        stage('move *.war file to Ansible server') { 
            steps { 
               sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible_host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }	
        stage('move Dockerfile file to Ansible server') { 
            steps { 
               sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible_host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /opt/docker
               docker build -t webapp_test .
               docker tag webapp_test srinku28/webapp_test
               sudo docker login -u srinku28 -p waheguru_28
               docker push srinku28/webapp_test
               docker rmi webapp_test srinku28/webapp_test''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'Dockerfile')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
			}
        }			
    }
}
