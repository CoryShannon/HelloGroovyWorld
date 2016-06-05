node {
   stage 'Setting git url'
	git url: 'https://github.com/CoryShannon/HelloGroovyWorld.git'
	stage 'Checking version'
	def v = version()
	if (v) {
		echo "Building version ${v}"
	}
	stage 'Setting maven tools'
	dev mvnHome = tool 'M3'
	sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
	stage 'Setting steps'
	step([$class: 'ArtifactArchiver', artifacts: '**/target/*.jar', fingerprint: true])
	step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
}
def version() {
	def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
	matcher ? matcher[0][1] : null
}
