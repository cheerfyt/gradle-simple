def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(label: label, cloud: 'kubernetes',
    containers: [
        containerTemplate(name: 'wtctl', image: 'worktile/wtctl:1.2.8', ttyEnabled: true, command: 'cat')
    ],
    volumes: [
        hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
        hostPathVolume(mountPath: '/tmp/cache', hostPath: '/tmp/cache/wt-rd-pipeline'),
    ]
) {
    node(label) {

        def scmVars = checkout scm
        def branch = scmVars.GIT_BRANCH

        stage('Using Worktile Pipeline') {
            script {
                container("wtctl") {
                    sh "wtctl"
                }
            }
        }
    }
 }