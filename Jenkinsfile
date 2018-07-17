import groovy.xml.*
import static java.util.UUID.randomUUID
def testName = "Jenkins"
timestamps {
    node("slave1") {
        stage('Checkout'){
        // Get some code from a GitHub repository
            git([url: 'https://github.com/OceanTest/Upload-Log-Test.git', branch: 'master'])        
        }
        
        def currentTestResults = [
                  "Passed_1", "Passed_2", "Passed_3"
                ]
        
        stage("GenerateXML") {
            writeFile(file: 'test.xml', text: resultsAsJUnit(currentTestResults))
            sh script: "ls"
             // publish html
            sh script: "pwd"
            archiveArtifacts(artifacts: 'test.xml', excludes: null)
            //currentBuild.description = currentBuild.description + "<br /></strong>${ParseToHTMLTable(command, params)}"
            step([
                  $class: 'JUnitResultArchiver',
                  testResults: '**/test.xml'
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
    testResults.each { test, testResult ->
      delegate.delegate.testsuite(name: test, tests: testResult.size(), failures: testResult.values().count(false)) {
        testResult.each { testName, testPassed ->
          delegate.delegate.testcase(name: testName) {
            if(!testPassed) { delegate.failure() }
          }
        }
      }
    }
  }
  return stringWriter.toString()
}
