#!groovy

node {
    stage 'Build'
    checkout scm
    withCredentials([
      [
       $class        : 'StringBinding',
       credentialsId : '8346e5a7-019d-4c8f-85ed-2cba663293e4',
       variable      : 'KSTOREPWD',
      ],
      [
       $class        : 'StringBinding',
       credentialsId : '8346e5a7-019d-4c8f-85ed-2cba663293e4',
       variable      : 'KEYPWD',
      ],
      [
       $class        : 'FileBinding',
       credentialsId : 'ce24f3f0-efe5-493c-bcad-e02df35a2c09',
       variable      : 'KEYSTORE',
      ],
    ]) {
        withEnv(["KSTOREPWD=${env.KSTOREPWD}", "KEYPWD=${env.KEYPWD}", "KEYSTORE=${env.KEYSTORE}", "LD_LIBRARY_PATH=/var/jenkins_home/tools/android-sdk/tools/lib", "ANDROID_HOME=/var/jenkins_home/tools/android-sdk"]) {
            sh "./gradlew clean assembleRelease"
        }
    }
    archiveArtifacts artifacts: 
    'app/build/outputs/apk/app-release.apk', excludes: null, 
    fingerprint: true, onlyIfSuccessful: true
}
