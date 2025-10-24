--- I use this commands to do Docker build ---

-- Stand in project root. This command creates the Docker Image  --
docker build -f dockerfile/Dockerfile.winems -t winems:v2.42.0n-test.1 .

-- This command run the docker in current terminal session if terminal is closed the docker stops --
docker run -it --rm -p 5000:80 winems:v2.42.0n-test.1

-- This command creates a docker container on the docker environment to run from there --
docker run -d -p 5000:80 --name winems-app winems:v2.42.0n-test.1

-- This command removes the docker container from docker environment --
docker rm winems-app

--- publish to Github GHCR ---

-- Github password needs to be added on machine --
- password must be Github token Personal access token (classic) -
- enable write:packages and delete:packages -
echo YOUR_GITHUB_PAT | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password TOKEN

docker tag winems:v2.42.0n-test.1 ghcr.io/winems/winems:v2.42.0n-test.1

docker push ghcr.io/winems/winems:v2.42.0n-test.1


--- Restoring a local db to Azure SQL server ---

Step 1: Restore the .bak file

You must first restore the .bak file to a local SQL Server instance. You can do this using SQL Server Management Studio (SSMS).

1. Open SSMS and connect to a SQL Server instance (either on-premises or on an Azure VM).

2. In Object Explorer, right-click on the Databases folder and select Restore Database....

3. In the "Restore Database" dialog, choose Device as the source and browse to your .bak file.

4. Specify a new name for the restored database under the Destination section and click OK to start the restore process.

Step 2: Export to .bacpac and Import to Azure

Once the database is restored, you can use SSMS or a migration tool to export it and import it into Azure SQL Database.

Using SQL Server Management Studio (SSMS)

1. In SSMS, right-click the newly restored database, go to Tasks, and select Export Data-tier Application....

2. Follow the wizard to save the database as a .bacpac file. You can save it locally or directly to an Azure Blob Storage container.

3. In the Azure portal, navigate to your Azure SQL server.

4. Click Import database from the top toolbar.

5. Select the storage account and the .bacpac file you created.

6. Specify the details for the new database, such as the name, service tier, and size.

7. Click Create to begin the import. A new database will be provisioned with the data from your .bacpac file.


Hello world test

dotnet publish --output "C:\Development\HelloWorldDotNetRelease"

docker build -f dockerfile/Dockerfile -t hwtest:v1-test.1 . 

docker run -it --rm -p 5000:5000 hwtest:v1-test.1