pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/i0679511023/DevOpsPipeine', branch: 'main')
      }
    }

    stage('Shell "ls"') {
      parallel {
        stage('Shell "ls"') {
          steps {
            sh 'ls -la '
          }
        }

        stage('package our application') {
          steps {
            sh '''FROM golang:alpine AS build-env
RUN mkdir /go/src/app && apk update && apk add git
ADD main.go /go/src/app/
WORKDIR /go/src/app
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -ldflags \'-extldflags "-static"\' -o app .

FROM scratch
WORKDIR /app
COPY --from=build-env /go/src/app/app .
ENTRYPOINT [ "./app" ]'''
          }
        }

      }
    }

  }
}