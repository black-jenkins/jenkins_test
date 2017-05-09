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
}
/* Accessible then with : params.release_tag, params.release_title ...  */
