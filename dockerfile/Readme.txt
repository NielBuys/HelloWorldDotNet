--- I use this commands to do Docker build ---


Hello world test

dotnet publish --output "C:\Development\HelloWorldDotNetRelease"

docker build -f dockerfile/Dockerfile -t hwtest:v1-test.1 . 

docker run -it --rm -p 5000:5000 hwtest:v1-test.1

-- Github password needs to be added on machine --
- password must be Github token Personal access token (classic) -
- enable write:packages and delete:packages -
echo YOUR_GITHUB_PAT | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password TOKEN

docker tag hwtest:v1-test.1 ghcr.io/nielbuys/helloworlddotnet/hwtest:v1-test.1

docker push ghcr.io/nielbuys/helloworlddotnet/hwtest:v1-test.1