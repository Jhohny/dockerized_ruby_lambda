# AWS Lambda Runtime Interface Emulator Setup

## x86-64 Architecture

To set up the runtime interface emulator for x86-64 architecture, follow these steps:

1. Create a directory for the emulator and download it from GitHub to your local machine:

   ```bash
   mkdir -p ~/.aws-lambda-rie && \
       curl -Lo ~/.aws-lambda-rie/aws-lambda-rie https://github.com/aws/aws-lambda-runtime-interface-emulator/releases/latest/download/aws-lambda-rie && \
       chmod +x ~/.aws-lambda-rie/aws-lambda-rie
   ```

## ARM64 Emulator

To set up the runtime interface emulator for ARM64 architecture, follow these steps:

1. Create a directory for the emulator and download it from GitHub to your local machine:

   ```bash
   mkdir -p ~/.aws-lambda-rie && \
       curl -Lo ~/.aws-lambda-rie/aws-lambda-rie https://github.com/aws/aws-lambda-runtime-interface-emulator/releases/latest/download/aws-lambda-rie-arm64 and chmod +x ~/.aws-lambda-rie/aws-lambda-rie
   ```

## Starting the Docker Image

Once you've set up the emulator, you can start the Docker image using the `docker run` command. Make sure to note the following:

- `docker-image:test` represents the image name and tag.
- `aws_lambda_ric lambda_function.LambdaFunction::Handler.process` specifies the `ENTRYPOINT` and `CMD` from your Dockerfile.

Here's an example command for both x86-64 and ARM64:

### x86-64 Example

```bash
DOCKER_DEFAULT_PLATFORM=linux/amd64 docker run -d -v ~/.aws-lambda-rie:/aws-lambda -p 9000:8080 \
    --entrypoint /aws-lambda/aws-lambda-rie \
    docker-image:test \
    aws_lambda_ric lambda_function.LambdaFunction::Handler.process
```

### ARM64 Example

```bash
DOCKER_DEFAULT_PLATFORM=linux/arm64 docker run -d -v ~/.aws-lambda-rie:/aws-lambda -p 9000:8080 \
    --entrypoint /aws-lambda/aws-lambda-rie \
    docker-image:test \
    aws_lambda_ric lambda_function.LambdaFunction::Handler.process
```

Replace `docker-image:test` with the appropriate image name and tag, and you're ready to run your containerized Lambda function.
```
