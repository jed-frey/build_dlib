pipeline {
  agent any
  stages {
    stage('DEBUG') {
      parallel {
        stage('pwd') {
          steps {
            sh 'pwd'
          }
        }
        stage('env') {
          steps {
            sh 'env'
          }
        }
      }
    }
    stage('Clone dlib') {
      steps {
        git(url: 'https://github.com/davisking/dlib.git', branch: 'master', changelog: true, poll: true)
      }
    }
    stage('Build dlib') {
      steps {
        sh 'rm -rf build; mkdir build; cd build; cmake .. -DUSE_AVX_INSTRUCTIONS=1; cmake --build .'
      }
    }
    stage('Build python library') {
      steps {
        sh 'python3 setup.py build'
      }
    }
  }
  environment {
    CUDA_PATH = '/usr/local/cuda-10.1'
  }
}