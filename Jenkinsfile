pipeline {
  agent {
    docker {
      image "node:8.12.0-stretch"
      args "--name media-restaurantetic \
            -w /app \
            --network restaurantetic \
            -p 9090:9090 \
            -v /var/www/media.restaurantetic.com/files:/app/files \
            -e MONGO_HOST=mongo-media-restaurantetic \
            -e MONGO_DB=restaurantetic \
            -e REDIS_HOST=redis-media-restaurantetic \
            -e KEY=${env.MEDIA_RESTAURANTETIC_KEY}"
    }
  }
  stages {
    stage ("Build") {
      steps {
        sh "npm install && npm run build"
      }
    }
    stage ("Run") {
      steps { 
        sh "npm run serve&"
        input message: "Finished using the web site? (Click \"Proceed\" to continue)"
      }
    }
  }
}