def testnode1 = env.testnode1
def testnode2 = env.testnode2
def Nodelist = [testnode1, testnode2]

def Tasks = [:]

node('slave1'){
    // Mark the code checkout 'stage'....
    stage('Checkout'){
        // Get some code from a GitHub repository
        git([url: 'https://github.com/OceanTest/Upload-Log-Test.git', branch: 'master'])
        
    }
    // Mark the code SSH upload'stage'....
    stage('SSH Test'){
    // Run the program
        sh script: "ssh root@10.18.134.106 'cd /home/ocean/ReadRetryCount/; ls'"
        sh script: "scp -r root@10.18.134.106:/home/ocean/ReadRetryCount/Readretrylog_20180710195812.txt /home/jenkins/workspace/Log_Upload_Test"
        sh script: "ls"
        archiveArtifacts artifacts: '**/*.txt', fingerprint: true        
        echo "ssh done"
        //               
    }  
}
