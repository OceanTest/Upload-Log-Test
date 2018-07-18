import groovy.xml.*
import static java.util.UUID.randomUUID
def testName = "Jenkins"
def numberOfBuild = '1'
timestamps {
    node("slave1") {
        stage('Checkout'){
        // Get some code from a GitHub repository
            git([url: 'https://github.com/OceanTest/Upload-Log-Test.git', branch: 'master'])        
        }
        Map builds = ["build_1":'passed', "build_2":'failed']
        stage("GenerateXML") {
            writeFile(file: 'ocean_test.xml', text: resultsAsJUnit(builds))
            sh script: "ls"
             // publish html
            sh script: "pwd"
            archiveArtifacts(artifacts: 'ocean_test.xml', excludes: null)
            step([
                  $class: 'JUnitResultArchiver',
                  testResults: '**/ocean_test.xml'
                ])
        }
    }
}
@NonCPS
String resultsAsJUnit(def testResults) {
    StringWriter  stringWriter  = new StringWriter()
    MarkupBuilder markupBuilder = new MarkupBuilder(stringWriter)
    // All those delegate calls here are messing up the elegancy of the MarkupBuilder
    // but are needed due to https://issues.jenkins-ci.org/browse/JENKINS-32766
    markupBuilder.testsuites {
        delegate.testsuite(name: "testName", tests: testResults.size(), failures: "1") {
            delegate.testcase(name: "testName", build_number: "1")            
        }
    }  
  return stringWriter.toString()
}
