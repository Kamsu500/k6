pipeline {
    agent {
        docker {
            image "grafana/k6"
            args "--entrypoint=''"  // Suppression du point d'entrée par défaut pour k6
        }
    }

    parameters {
        choice(name: 'CHOICE', choices: ['script.js', 'posts_e2e.postman_collection.js'], description: 'Choisir la collection')
        string(name: 'TEMPS_STAGE_1', defaultValue: '1m', description: 'Choisir le temps stage 1')
        string(name: 'CHARGE_STAGE_1', defaultValue: '200', description: 'Choisir la charge stage 1')
        string(name: 'TEMPS_STAGE_2', defaultValue: '2m', description: 'Choisir le temps stage 2')
        string(name: 'CHARGE_STAGE_2', defaultValue: '200', description: 'Choisir la charge stage 2')
        string(name: 'TEMPS_STAGE_3', defaultValue: '30s', description: 'Choisir le temps stage 3')
        string(name: 'CHARGE_STAGE_3', defaultValue: '0', description: 'Choisir la charge stage 3')
    }

    stages {
        stage('Vérification de la version de k6') {
            steps {
                sh 'k6 -v'  // Vérification de la version de k6
            }
        }

        stage('Exécuter les tests k6') {
            steps {
                script {
                    // Construction de la commande k6 avec les paramètres passés
                    def command = "k6 run --stage ${params.TEMPS_STAGE_1}:${params.CHARGE_STAGE_1} " +
                                  "--stage ${params.TEMPS_STAGE_2}:${params.CHARGE_STAGE_2} " +
                                  "--stage ${params.TEMPS_STAGE_3}:${params.CHARGE_STAGE_3} " +
                                  "${params.CHOICE}"
                    sh command
                }
            }
        }
    }
}
