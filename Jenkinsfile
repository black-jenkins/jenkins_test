properties([
  parameters([
    string(name: 'release_tag', defaultValue: '', description: 'Please enter the tag version for the release.'),
    string(name: 'release_title', defaultValue: '', description: 'Please enter the release title.'),
    text(name: 'release_desc', defaultValue: '', description: 'Please describe this release.'),
    booleanParam(name: 'pre_release', defaultValue: true, description: 'Please identify the release state. By default the release is set as a pre-release.'),
  ])
])

node {
  stage 'Create tag and release'
  echo params.release_tag
  echo params.release_title
  
  withCredentials([
    [$class: 
      'UsernamePasswordMultiBinding',
      credentialsId: 'GITHUB_REPO_AUTH',
      usernameVariable: 'GITHUB_REPO_USER',
      passwordVariable: 'GITHUB_REPO_TOKEN'
    ]
  ]) {
    try {
      sh '''github-release release \\
        --security-token env.GITHUB_REPO_TOKEN
        --user env.GITHUB_REPO_USER \\
        --repo jenkins_test \\
        --tag params.release_tag \\
        --name params.release_title \\
        --description params.release_desc \\
        --pre-release'''
    }
    catch (err) {
      throw err
    }
  }
}

/* Accessible then with : params.release_tag, params.release_title ...  */
