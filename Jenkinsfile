def CD_IP = env.CD_IP

node('slave1'){
    // Mark the code checkout 'stage'....
    stage('Checkout'){
        // Get some code from a GitHub repository
        git([url: 'https://github.com/OceanTest/Upload-Log-Test.git', branch: 'master'])
        
    }
    stage('Do FIO Retry Test'){
        // Run the program
        sh script:"ssh ${CD_IP} 'cd /home/ocean/ReadRetryCount;python rdrery_test.py'"
    }
    // Mark the code SSH upload'stage'....
    stage('Upload Log'){
    // Run the program
        sh script: "ssh ${CD_IP} 'cd /home/ocean/ReadRetryCount/; ls'"
        sh script: "scp -r ${CD_IP}:/home/ocean/ReadRetryCount/Readretrylog_*.txt /home/jenkins/workspace/Log_Upload_Test"
        sh script: "ls"
        archiveArtifacts artifacts: '**/*.txt', fingerprint: true        
        echo "ssh done"
        //               
    }  
}
