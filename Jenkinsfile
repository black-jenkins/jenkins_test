properties([
  parameters([
    string(defaultValue: '', description: 'Please enter the tag version for the release.', name: 'release_tag'),
    string(defaultValue: '', description: 'Please enter the release title.', name: 'release_title'),
    text(defaultValue: 'Please describe this release.', description: '', name: 'release_description'),
    booleanParam(defaultValue: true, description: 'Please identify the release state. By default the release is set as a pre-release.', name: 'pre_release'),
  ])
])

/* Accessible then with : params.release_tag, params.release_title...  */
