# ie11-workarounds
A place to store easily forgotten IE11 workarounds

[FormData]{#formdata-submission-error}

## FormData() Submission Error
### Situation
This popped up for me when trying to push up a PDF file only to a server via a REST API end point using JavaScript. The server comes back with an error. We found that the "FormData" string is being corrupted/invalid by IE11 and is therefore unusable by the server.
```javscript
uploadPDF() {
  var file = fileFieldValue.info[0]
  var reader = new FileReader()
  
  if (file) reader.readAsDataURL(file)

  var payload = new FormData()
  payload.append('pendingorderPDF', file)
  // ... send file to server
}
```
### Fix
Simply append another empty value to the server before sending the FormData
```javscript
uploadPDF() {
  var file = fileFieldValue.info[0]
  var reader = new FileReader()
  
  if (file) reader.readAsDataURL(file)

  var payload = new FormData()
  payload.append('pendingorderPDF', file)
  payload.append('hidden', '')
  // ... send file to server
}
```

### Resources
[Here]{https://blog.yorkxin.org/2014/02/06/ajax-with-formdata-is-broken-on-ie10-ie11} Describes some more situations and workarounds.
