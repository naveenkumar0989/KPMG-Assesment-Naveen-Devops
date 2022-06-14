node{											
    def buildnumber=BUILD_NUMBER											
    stage('Checkoutspringbootcode'){											
        git branch: 'development', url: 'https://github.com/naveenkumar0989/********(reponame).git'											
    }											
    stage('Buildpackageforspringbootapplication'){											
        def MavenHome= tool name: 'Maven-3.6.3',type: 'maven'											
        sh "${MavenHome}/bin/mvn clean package"											
    }											
    stage ('CreateImage from Buildpackage'){											
        sh "docker build -t ************.dkr.ecr.ap-south-1.amazonaws.com/spring-boot-mongo-kubernetes:${buildnumber} ."											
    }											
    stage ('Login and push the Image'){											
        sh "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin *************.dkr.ecr.ap-south-1.amazonaws.com"											
       sh "docker push **********.dkr.ecr.ap-south-1.amazonaws.com/spring-boot-mongo-kubernetes:${buildnumber} "											
   }											
    }											
    stage("Deploy To Kuberates Cluster"){
       kubernetesDeploy(
         configs: 'springBootMongo.yml', 
         kubeconfigId: 'KUBERNATES_CONFIG',
         enableConfigSubstitution: true													
											
    }											
}											
