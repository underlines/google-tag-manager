

```
<script>
  var uaid =  'UA-XXXXXXXXXX-1';
  // set the id of your hidden form field for clientId and gclid
  // if you have more than one form on a single page, you can name further fields with the same name + a number from 1 to 4, so for example:
  // <form><field id="clientId">
  // <form><field id="clientId1">
  // <form><field id="clientId2">
  // the script will automatically iterate through up to 5 forms on a single page
  
  var clientIdFieldId = 'form-field-clientId'; //add base name, without number
  var gclidFieldId = 'form-field-gclid'; //add base name, without number
  
  var gclid = {{Cookie - gclid}}; // name of your GTM variable
  
  // get Google Analytics clientId of current user -> https://stackoverflow.com/questions/20053949/how-to-get-the-google-analytics-client-id/20054201#20054201
  var clientId = '';
  try {
    var trackers = ga.getAll();
    for (var i = 0; i < trackers.length; i++) {
      if (trackers[i].get('trackingId') === uaid) {
        clientId = trackers[i].get('clientId');
        //console.log('DEBUG: get clientId = '+clientId);
        break;
      }
    }
  } catch(e) {}
  
// Find the fields for up to 5 forms the page, then read gclid from and clientId from the cookie and sets it in the fields, when the user submits a form:
for (i = 0; i < 5; i++) {
  var j=i;
  if(i===0){
    j=""; // we want to look for "fieldname", not "fieldname0" below
  }
  try {
    //console.log('DEBUG: set form fields id = "' + gclidFieldId + j + '" to value = "' + gclid + '"');
    //console.log('DEBUG: set form fields id = "' + clientIdFieldId + j + '" to value = "' + clientId + '"');
    document.getElementById(gclidFieldId+j).value = gclid;
	  document.getElementById(clientIdFieldId+j).value = clientId;
  }
  catch(e) {
    break;
  }
}
</script>
```
