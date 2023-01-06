# Project-Management-Form



<html lang="en">
<head>
<title>Bootstrap Example</title>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet"
href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
<script
src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script
src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
<script
src=<script
src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>></script>
</head>
<body>
<div class="container">
<h2>Project Management Form</h2>
<form id="projectForm" method="post">
<div class="form-group">
<span><label for="ProjectId">Project ID:</label> <label id="projectIdMsg">
</label></span>
<input type="text" class="form-control" name="projectId" id="projectId"
placeholder="Enter Project ID" required>
</div>
<div class="form-group">
<label for="projectName">Project Name:</label>
<input type="text" class="form-control" id="projectName"
placeholder="Enter Project Name" name="projectName">
</div>
<div class="form-group">
<label for="projectAssignedTo">Assigned To:</label>
<input type="Assigned To" class="form-control" id="projectAssignedTo"
placeholder="Enter Assigned To" name="projectAssignedTo">
</div>
<div class="form-group">
<label for="projectAssignmentDate">Assignment Date:</label>
<input type="Assigned Date" class="form-control" id="projectAssignmentDate"
placeholder="Enter Assignment Date" name="projectAssignmentDate">
</div>
<div class="form-group">
 <label for="projectDeadline">Deadline:</label>
<input type="Deadline" class="form-control" id="projectDeadline"
placeholder="Deadline" name="projectDeadline">
</div>
<input type="button" class="btn btn-primary" id="projectSave" value="Save"
onclick="saveProject();">
</form>
</div>
<script>
$("#projectId").focus();
function validateAndGetFormData() {
var projectIdVar = $("#projectId").val();
if (projectIdVar === "") {
alert("Project ID Required Value");
$("#projectId").focus();
return "";
}
var projectNameVar = $("#projectName").val();
if (projectNameVar === "") {
alert("Project Name is Required Value");
$("#projectName").focus();
return "";
}
var projectAssignedToVar = $("#projectAssignedTo").val();
if (projectAssignedToVar === "") {
alert("Assigned To is Required Value");
$("#projectAssignedTo").focus();
return "";
}
var projectAssignmentDateVar = $("#projectAssignmentDate").val();
if (projectAssignmentDate === "") {
alert("Assigned Date is Required Value");
$("#projectAssignmentDate").focus();
return "";
}
var projectDeadlineVar = $("#projectDeadline").val();
if (projectDeadline === "") {
alert("Deadline is Required Value");
$("#projectDeadline").focus();
return "";
}

var jsonStrObj = {
projectId: projectIdVar,
projectName: projectNameVar,
projectAssignedTo: projectAssignedToVar,
projectAssignmentDate: projectAssignmentDateVar,
projectDeadline: projectDeadlineVar,

};
return JSON.stringify(jsonStrObj);
}
// This method is used to create PUT Json request.
function createPUTRequest(connToken, jsonObj, dbName, relName) {
var putRequest = "{\n"
+ "\"token\" : \""
+ connToken
+ "\","
+ "\"dbName\": \""
+ dbName
+ "\",\n" + "\"cmd\" : \"PUT\",\n"
+ "\"rel\" : \""
+ relName + "\","
+ "\"jsonStr\": \n"
+ jsonObj
+ "\n"
+ "}";
return putRequest;
}
function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
var url = dbBaseUrl + apiEndPointUrl;
var jsonObj;
$.post(url, reqString, function (result) {
jsonObj = JSON.parse(result);
}).fail(function (result) {
var dataJsonObj = result.responseText;
jsonObj = JSON.parse(dataJsonObj);
});
return jsonObj;
}
function resetForm() {
$("#projectId").val("")
$("#projectName").val("");
$("#projectAssignedTo").val("");
$("#projectAssignmentDate").val("");
$("#projectDeadline").val("");
$("#projectId").focus();
}
function saveProject() {
var jsonStr = validateAndGetFormData();
if (jsonStr === "") {
return;
}
var putReqStr = createPUTRequest("90932467|-31949270643621304|90955412",
jsonStr, "COLLEGE-DB", "PROJECT-TABLE");
alert(putReqStr);
jQuery.ajaxSetup({async: false});
var resultObj = executeCommand(putReqStr,
"http://api.login2explore.com:5577", "/api/iml");
alert(JSON.stringify(resultObj));
jQuery.ajaxSetup({async: true});
resetForm();
}
</script>
</body>
</html>
