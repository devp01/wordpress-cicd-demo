pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/YOUR_USERNAME/wordpress-cicd-demo.git'
            }
        }

        stage('Deploy Theme') {
            steps {
                sh '''
                sudo rm -rf /var/www/html/wordpress/wp-content/themes/my-cicd-theme
                sudo cp -r theme/my-cicd-theme /var/www/html/wordpress/wp-content/themes/
                sudo chown -R www-data:www-data /var/www/html/wordpress/wp-content/themes/my-cicd-theme
                '''
            }
        }

        stage('Success Message') {
            steps {
                echo 'Deployment Completed Successfully!'
            }
        }
    }
}
