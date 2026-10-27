pipeline {
    agent any

    parameters {
        choice(name: 'ENTORNO', choices: ['QA', 'PROD'], description: 'Selecciona el entorno de AWS')
        booleanParam(name: 'DESTRUIR', defaultValue: false, description: '¿Marcar para destrucción de recursos?')
    }

    stages {
        stage('Despliegue QA') {
            when {
                expression { params.ENTORNO == 'QA' }
            }
            steps {
                echo 'Desplegando infraestructura en QA (us-east-1)...'
                // sh 'aws cloudformation deploy ...'
            }
        }

        stage('Despliegue PROD') {
            when {
                expression { params.ENTORNO == 'PROD' }
            }
            steps {
                input message: 'ALERTA: Se afectará Producción. ¿Estás seguro?', ok: 'Aprobar PROD'
                echo 'Desplegando infraestructura en PROD (eu-west-1)...'
            }
        }

        stage('Destrucción') {
            when {
                expression { params.DESTRUIR == true }
            }
            steps {
                echo "⚠️ ELIMINANDO recursos del entorno: ${params.ENTORNO}"
                // sh 'aws cloudformation delete-stack ...'
            }
        }
    }
}
