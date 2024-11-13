pipeline {
    agent any

    stages {
        stage('stage-1') {
            steps {
                   sh '''#!/bin/bash
cat <<EOF > index.php
<?php
echo "<h1>Welcome to My Sample PHP Page!</h1>";
echo "<p>This is a sample Dockerized PHP application.</p>";
EOF
echo "Indexfile created:"
cat index.php'''
                    
            }
        }
        stage('stage-2')  {
            steps {
                    sh '''#!/bin/bash
cat <<EOF > Dockerfile
# Use the official PHP image with Apache
FROM php:8.1-apache

# Copy the PHP file to the Apache web directory
COPY index.php /var/www/html/

# Expose port 80
EXPOSE 80

# Start Apache in the foreground
CMD ["apache2-foreground"]
EOF
echo "Dockerfile created:"
ls -la
cat Dockerfile'''
                  }
             }
stage('stage-3')  {
            steps {
                    sh '''#!/bin/bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 503561451240.dkr.ecr.ap-south-1.amazonaws.com


docker build -t  clado-pipjen:p2 .

docker tag clado-pipjen:p2 503561451240.dkr.ecr.ap-south-1.amazonaws.com/clado-pipjen:p2

docker push 503561451240.dkr.ecr.ap-south-1.amazonaws.com/clado-pipjen:p2
'''

            }
        }
    }
}
