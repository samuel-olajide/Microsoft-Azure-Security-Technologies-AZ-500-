# Lab scenario

You have been asked to create a proof of concept application that makes use of the Azure SQL Database support for Always Encrypted functionality. All of the secrets and keys used in this scenario should be stored in Key Vault. The application should be registered in Microsoft Entra ID in order to enhance its security posture. To accomplish these objectives, the proof of concept should include:
  - Creating an Azure Key Vault and storing keys and secrets in the vault.
  - Create a SQL Database and encrypting content of columns in database tables by using Always Encrypted.

To keep the focus on the security aspects of Azure, related to building this proof of concept, you will start from an automated ARM template deployment, setting up a Virtual Machine with Visual Studio and SQL Server Management Studio.
