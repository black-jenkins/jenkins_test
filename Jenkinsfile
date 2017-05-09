env.GITHUB_RELEASE_FILE_NAME = "file_upload_test.txt"
env.GITHUB_RELEASE_FILE_DESC = "This is a description of uploaded file."
env.GITHUB_RELEASE_FILE_PATH = "~/workspace/file_upload_test.txt"

properties([
  parameters([
    string(name: 'GITHUB_RELEASE_TAG', defaultValue: '', description: 'Please enter the tag version for the release.'),
    string(name: 'GITHUB_RELEASE_TITLE', defaultValue: '', description: 'Please enter the release title.'),
    text(name: 'GITHUB_RELEASE_DESC', defaultValue: '', description: 'Please describe this release.'),
    booleanParam(name: 'GITHUB_RELEASE_STATE', defaultValue: true, description: 'Please identify the release state. By default the release is set as a pre-release.'),
  ])
])

node {
  stage 'Create tag and release'
  
  withCredentials([
    [$class: 'UsernamePasswordMultiBinding', credentialsId: 'GITHUB_REPO_AUTH', usernameVariable: 'GITHUB_REPO_USER', passwordVariable: 'GITHUB_REPO_TOKEN']
  ]) {
    try {
      stage 'Dump some stuff'
      sh 'env > env.txt' 
      for (String i : readFile('env.txt').split("\r?\n")) {
        println i
      }

      stage 'Create release'
      sh '''github-release release \
        --security-token ${GITHUB_REPO_TOKEN} \
        --user ${GITHUB_REPO_USER} \
        --repo ${GITHUB_REPO_NAME} \
        --tag ${GITHUB_RELEASE_TAG} \
        --name "${GITHUB_RELEASE_TITLE}" \
        --description "${GITHUB_RELEASE_DESC}" \
        --pre-release'''
        
      stage 'Upload file'
      sh '''github-release upload \
        --security-token ${GITHUB_REPO_TOKEN} \
        --user ${GITHUB_REPO_USER} \
        --repo ${GITHUB_REPO_NAME} \
        --tag ${GITHUB_RELEASE_TAG} \
        --name "${GITHUB_RELEASE_FILE_NAME}" \
        --label "${GITHUB_RELEASE_FILE_DESC}" \
        --file ${GITHUB_RELEASE_FILE_PATH}'''
    }
    catch (err) {
      throw err
    }
  }
}
