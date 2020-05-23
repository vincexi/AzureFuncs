# AzureFuncs
A license payment processing set of azure functions using various triggers and bindings to perform cascading actions 

OnPaymentReceived function contains a POST endpoint receiving the Order model. The order is recorded to Azure Storage and then added to a Queue.

GenerateLicenseFile function is an async task with a Queue trigger that generates a license file.

EmailLicenseFile function is a blob trigger that fires once it see a new license file is generated. It compiles an email using SendGrid Azure Extension to send to the order email.

To run this, you will need to create a free account with SendGrid for an API key and verify a sender email. Input the two value in local.settings.json

{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet",
    "EmailSender": "",
    "SendGridApiKey": ""
  }
}
