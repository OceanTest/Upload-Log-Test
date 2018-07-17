import groovy.xml.*
import static java.util.UUID.randomUUID
def testName = "Jenkins"
timestamps {
    node("slave1") {
        stage("GenerateXML") {
            writeFile(file: 'test.xml', text: ParseToHTMLTable(['X', 'Y', 'Z'], 3))
            sh script: "ls"
             // publish html
            sh script: "pwd"
            archiveArtifacts(artifacts: 'test.xml', excludes: null)
            currentBuild.description = currentBuild.description + "<br /></strong>${ParseToHTMLTable(command, params)}"
        }
    }
}
@NonCPS
def ParseToHTMLTable(columns, rowCount) {
    def writer = new StringWriter()
    def markupBuilder = new MarkupBuilder(writer)
    markupBuilder.table(style: 'border:1px solid;text-align:center;') {
        (1..rowCount).each { row ->
            delegate.delegate.tr {
                delegate.td(row)
                columns.each {delegate.delegate.td((Math.random() * 9999) as int ) }
            }
        }       
    }
    echo "Bug Here???"
    return writer.toString()
}

