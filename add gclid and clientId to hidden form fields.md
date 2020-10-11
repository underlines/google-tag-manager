# GTM configuration:
## Variables
Create the following new variables
### URL Param - gclid
- Variable Name: `URL Param - gclid`
- Type: `URL`
- Component Type: `Query`
- Query Key: `gclid`

### Cookie - gclid
- Variable Name: `Cookie - gclid`
- Type: `1st-Party Cookie`
- Cookie Name: `gclid`

### JS - Helper - Create Cookie
- Variable Name: `JS - Helper - Create Cookie`
- Type: `Custom JavaScript`
- Custom JavaScript:
```
function() {
  return function(name, value, ms, path, domain) {
    if (!name || !value) {
      return;
    }
    var d;
    var cpath = path ? '; path=' + path : '';
    var cdomain = domain ? '; domain=' + domain : '';
    var expires = '';
    if (ms) {
      d = new Date();
      d.setTime(d.getTime() + ms);
      expires = '; expires=' + d.toUTCString();
    }
    document.cookie = name + "=" + value + expires + cpath + cdomain;
  }
}
```
## Triggers
Create the following new trigger:

### Pageview - gclid set in url
- Trigger Name: `Pageview - gclid set in url`
- Trigger Type: `Page View`
- This trigger fires on: `Some Page Views`
- Conditions: `URL Param - gclid` >> `does not match RegEx (ignore case)` >> `^(undefined|null|0|false|NaN|)$`

## Tags
Create the following tags:

### cHTML - create Cookie - gclid
- Tag Name: `cHTML - create Cookie - gclid`
- Tag Type: `Custom HTML`
- HTML:
```
<script>
  {{JS - Helper - Create Cookie}}('gclid', '{{URL Param - gclid}}', 15552000000, '/', undefined);
</script>
```
Firing Triggers: `Pageview - gclid set in url`


### cHTML - form Submission - add clientId & gclid to hidden field
- Tag Name: `cHTML - form Submission - add clientId & gclid to hidden field`
- Tag Type: `Custom HTML`
- HTML:
```
<script>
  var uaid =  'UA-XXXXXXXXXX-1';
  var clientIdFieldId = 'form-field-clientId';
  var gclidFieldId = 'form-field-gclid';
  var gclid = {{Cookie - gclid}};
  var numForms = 1;
  
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
for (i = 0; i < numForms; i++) {
  var j=i;
  if(i===0){
    j=""; // we want to look for "fieldname", not "fieldname0" in the first iteration
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

#### Configuration of the script
You need to edit the top part of the script, like explained below:
**uaid**
`var uaid = 'UA-XXXXXXXXXX-1';`

Set your Google Analytics Property ID 

**clientIdFieldId**
`var clientIdFieldId = 'form-field-clientId';`

Set the id of your website form hidden field for clientId and gclid

**gclidFieldId**
`var gclidFieldId = 'form-field-gclid';`

Same as 2. but for Google Ads Click ID

**GTM Variable for gclid**
`var gclid = {{Cookie - gclid}};`

Set the name of your Cookie Variable in your GTM that you created in the steps above, if you followed the whole tutorial and used it's name, you don't have to change anything here

**numForms**
`var numForms = 3;`

If you have only one form on the page, set this to 1, otherwise set it to a number higher than 1.
name the field ids like in the following example:
```
<form><field id="clientId">...
<form><field id="clientId1">...
<form><field id="clientId2">...
```
In this example you would have to set `numForms = 3`
The script will automatically iterate through all of them. Ask your developer to help you, if you don't know how to set or find your hidden field IDs
