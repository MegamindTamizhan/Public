# To connect to an Azure Blob Storage container in your Java application using an access key, follow these steps:

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

## 3. Authorize Access and Connect to Blob Storage

* Import Required Classes:
  * Add the necessary import statements in your Java file:
```
import com.azure.storage.blob.*;
import com.azure.storage.blob.models.*;
import com.azure.storage.common.StorageSharedKeyCredential;
```
* Create a BlobServiceClient:
 * Use the storage account name and access key to authenticate:

```
String accountName = "<your-storage-account-name>";
String accountKey = "<your-storage-account-key>";
StorageSharedKeyCredential credential = new StorageSharedKeyCredential(accountName, accountKey);

BlobServiceClient blobServiceClient = new BlobServiceClientBuilder()
    .endpoint("https://" + accountName + ".blob.core.windows.net")
    .credential(credential)
    .buildClient();
```
* Get a Reference to the Container:
 * Access your container:

```
BlobContainerClient containerClient = blobServiceClient.getBlobContainerClient("<your-container-name>");
```

## 4. Upload and Download Blobs

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

## 5. Run Your Application

* Compile and run your application to ensure it connects to Azure Blob Storage and performs the upload/download operations.
