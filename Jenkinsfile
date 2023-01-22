pipeline{
    agent none
    environment{
        AUTHOR = "Rapli Maulana Aji"
        EMAIL = "rapli.maulana@gmail.com"
    }
    stages{
        stage("Prepare"){
            environment{
                APP = credentials("maulana_rahasia")                 #mengambil data pada credential dengan ID 'maulana_rahasia'. Secara otomatis username akan menjadi APP_USR dan password menjadi APP_PSW
            }
            agent{
                node{
                    label "linux && java11"
                }
            }
            steps{
                echo("Author : ${AUTHOR}")
                echo("Email : ${EMAIL}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
                echo("App User : ${APP_USR}")
                echo("App Password : ${APP_PSW}")
            }
        }
        stage("Build"){
            agent{
                node{
                    label "linux && java11"
                }
            }
            steps{
                script{
                    for (int i=0; i<10; i++){
                        echo("Script ${i}")
                    }
                }
                echo("Start Build")
                sh("./mvnw clean compile test-compile")
                echo("Finish Build")
            }
        }
        stage("Test"){
            agent{
                node{
                    label "linux && java11"
                }
            }
            steps{
                script{
                    def data = [
                        "FirstName" : "Rapli",
                        "LastName"  : "Maulana"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
                echo("Start Build")
                echo("./mvnw test")
                echo("Finish Build")
                }
            }
        stage("Deploy"){
            agent{
                node{
                    label "linux && java11"
                }
            }
            steps{
                echo("Hello Deploy 1")
                sleep(5)
                echo("Hello Deploy 2")
            }
        }
    }
    post{
        always{
            echo "I will always say Hello again"
        }
        success{
            echo "Yeay, success"
        }
        failure{
            echo "Oh no, failure"
        }
        cleanup{
            echo "Don't care success or error"
        }
    }
}
