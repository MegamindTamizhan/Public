# To connect to an Azure Blob Storage container in your Java application using a Shared Access Signature (SAS), follow these steps:

## 1. Prerequisites:

* Azure Subscription: Ensure you have an active Azure subscription.
* Azure Storage Account: Create a storage account and a container.
* Java Development Kit (JDK): Version 8 or above.
* Apache Maven: For project management.

## 2. Set Up Your Project

* Create a Maven Project:
  * Use your IDE or command line to create a new Maven project.
* Add Dependencies:
  * Open the `pom.xml` file and add the following dependencies:
```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>com.azure</groupId>
      <artifactId>azure-sdk-bom</artifactId>
      <version>1.0.0</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
<dependencies>
  <dependency>
    <groupId>com.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
  </dependency>
</dependencies>
```

## 3. Generate a SAS Token

* Generate SAS Token
  * You can generate a SAS token using the Azure Portal, Azure CLI, or Azure SDKs. Here’s an example using Azure CLI:
```
az storage blob generate-sas \
  --account-name <your-storage-account-name> \
  --container-name <your-container-name> \
  --permissions rwdlac \
  --expiry <expiry-date> \
  --output tsv
```

| Replace `<your-storage-account-name>`, `<your-container-name>`, and `<expiry-date>` with your actual values.

## 4. Connect to Blob Storage Using SAS Token

* Import Required Classes:
  * Add the necessary import statements in your Java file:
```
import com.azure.storage.blob.*;
import com.azure.storage.blob.models.*;
```

* Create a BlobServiceClient:
  * Use the SAS token to authenticate:
```
String sasToken = "<your-sas-token>";
String blobServiceUrl = "https://<your-storage-account-name>.blob.core.windows.net";
BlobServiceClient blobServiceClient = new BlobServiceClientBuilder()
    .endpoint(blobServiceUrl)
    .sasToken(sasToken)
    .buildClient();
```
* Get a Reference to the Container:
  * Access your container:
```
BlobContainerClient containerClient = blobServiceClient.getBlobContainerClient("<your-container-name>");
```

## 5. Upload and Download Blobs

* Upload a Blob:
  * Upload a file to the container:
```
BlobClient blobClient = containerClient.getBlobClient("sample-blob.txt");
blobClient.uploadFromFile("path/to/local/file.txt");
```

* Download a Blob:
  * Download a file from the container:

```
blobClient.downloadToFile("path/to/downloaded/file.txt");
```

## 6. Run Your Application

* Compile and run your application to ensure it connects to Azure Blob Storage and performs the upload/download operations.
