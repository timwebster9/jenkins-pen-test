pipeline {

  agent {
    kubernetes {
      label 'k8s'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: kali
    image: timwebster9/kali-linux:latest
    command:
    - cat
    tty: true
  - name: msp
    image: timwebster9/metasploit:latest
    command:
    - cat
    tty: true
"""
    }
  }
    stages {
        stage('Port Scan (Kali Image)') {
            steps {
                container('kali') {
                    sh 'msfconsole -n -q -r /probe/resourceFile.txt'
                }
            }
        }
        stage('Port Scan (Metasploit Image)') {
            steps {
                container('msp') {
                    sh '/usr/src/metasploit-framework/msfconsole -n -q -r /probe/resourceFile.txt'
                }
            }
        }
    }
}