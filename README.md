<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Get Server Certificate</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }
    .output {
      margin-top: 20px;
      white-space: pre-wrap;
      background: #f0f0f0;
      padding: 10px;
      border: 1px solid #ccc;
      max-width: 600px;
    }
  </style>
</head>
<body>

<h1>Get SSL Certificate Information</h1>
<p>Enter a server hostname (e.g., google.com) to retrieve its SSL certificate.</p>

<form id="certForm">
  <label for="hostname">Hostname: </label>
  <input type="text" id="hostname" name="hostname" required>
  <button type="submit">Get Certificate</button>
</form>

<div id="certificateOutput" class="output"></div>

<script>
  document.getElementById('certForm').addEventListener('submit', function(event) {
    event.preventDefault();
    
    const hostname = document.getElementById('hostname').value;
    const outputDiv = document.getElementById('certificateOutput');
    outputDiv.textContent = "Loading...";

    // Replace with your hosted API URL
    const apiUrl = `https://your-api-app.herokuapp.com/get_certificate?hostname=${hostname}`;
    
    fetch(apiUrl)
      .then(response => response.json())
      .then(data => {
        if (data.certificate) {
          outputDiv.textContent = `Certificate for ${hostname}:\n${data.certificate}`;
        } else {
          outputDiv.textContent = "Error: " + (data.error || "Unknown error");
        }
      })
      .catch(error => {
        outputDiv.textContent = "Error: " + error.message;
      });
  });
</script>

</body>
</html>
