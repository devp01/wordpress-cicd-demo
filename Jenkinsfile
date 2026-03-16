pipeline {
    agent any

    environment {
        WP_DIR = "/var/www/html/wordpress"
        THEME_DIR = "/var/www/html/wordpress/wp-content/themes/my-cicd-theme"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/devp01/wordpress-cicd-demo.git'
            }
        }

        stage('Install WordPress if Missing') {
            steps {
                sh '''
                if [ ! -f "$WP_DIR/index.php" ]; then
                    cd /tmp
                    wget https://wordpress.org/latest.tar.gz
                    tar -xzf latest.tar.gz

                    sudo rm -rf $WP_DIR
                    sudo mkdir -p $WP_DIR
                    sudo cp -r wordpress/* $WP_DIR/
                    sudo chown -R www-data:www-data $WP_DIR
                fi
                '''
            }
        }

        stage('Deploy Theme') {
            steps {
                sh '''
                sudo rm -rf $THEME_DIR
                sudo mkdir -p $THEME_DIR
                sudo cp -r my-cicd-theme/* $THEME_DIR/
                sudo chown -R www-data:www-data $THEME_DIR
                '''
            }
        }

        stage('Verify Site') {
            steps {
                sh 'curl -I http://34.238.248.222/wordpress/'
            }
        }
    }
}
