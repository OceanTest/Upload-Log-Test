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
    // Mark the code GetParameter 'stage'....
    stage('GetParameterviaEnvironment'){
    // Run the program
        sh script "scp -r /home/ocean/ReadRetryCount/Readretrylog_20180710195812.txt root@10.25.132.128:~/Workspace              
        }
    }
    
    
}


