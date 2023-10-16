x86-64 architecture
From your project directory, run the following command to download the runtime interface emulator (x86-64 architecture) from GitHub and install it on your local machine.

mkdir -p ~/.aws-lambda-rie && \
    curl -Lo ~/.aws-lambda-rie/aws-lambda-rie https://github.com/aws/aws-lambda-runtime-interface-emulator/releases/latest/download/aws-lambda-rie && \
    chmod +x ~/.aws-lambda-rie/aws-lambda-rie


arm64 emulator
From your project directory, run the following command to download the runtime interface arm64 emulator from GitHub and install it on your local machine.

mkdir -p ~/.aws-lambda-rie && \
    curl -Lo ~/.aws-lambda-rie/aws-lambda-rie https://github.com/aws/aws-lambda-runtime-interface-emulator/releases/latest/download/aws-lambda-rie-arm64 && \
    chmod +x ~/.aws-lambda-rie/aws-lambda-rie


Start the Docker image with the docker run command. Note the following:
docker-image is the image name and test is the tag.
aws_lambda_ric lambda_function.LambdaFunction::Handler.process is the ENTRYPOINT followed by the CMD from your Dockerfile.

docker run -d -v ~/.aws-lambda-rie:/aws-lambda -p 9000:8080 \
    --entrypoint /aws-lambda/aws-lambda-rie \
    docker-image:test \
        aws_lambda_ric lambda_function.LambdaFunction::Handler.process

my sample:
DOCKER_DEFAULT_PLATFORM=linux/amd64 docker run -d -v ~/.aws-lambda-rie:/aws-lambda -p 9000:8080 \
    --entrypoint /aws-lambda/aws-lambda-rie \
    39b18030a799 \
        aws_lambda_ric lambda_function.LambdaFunction::Handler.process
