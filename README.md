<h1 align="center">Go Lambda SNS Example</h1>

An example of creating a Go Lambda function, an SNS Topic and subscribing the Lambda to the newly created topic.  
You can change the names and descriptions of the Function, Topic etc.

## Deployment
In order to deploy this you need to compile your Go Lambda function and upload it to S3 as a `.zip` file.  
You then need to update your functions `CodeUri` in the CloudFormation `template.yaml` file to point to the bucket where 
you uploaded the zipped Lambda function to.

[AWS Docs](https://docs.aws.amazon.com/lambda/latest/dg/golang-package.html)  
A .zip file archive is a deployment package for your Lambda function that consists of your code (a Go executable) and any dependencies.

After you create the deployment package, you can upload it directly to an AWS S3 bucket in the Region where you want to create the Lambda function. Or, you can upload the `.zip` file archive first and then specify the S3 bucket name and object key name when you create the function using the Lambda console or the AWS CLI.

### Unix
Download the Lambda library for Go with go get, and compile your executable.
```shell
~/my-function$ go get github.com/aws/aws-lambda-go/lambda
~/my-function$ GOOS=linux go build main.go
```
Setting `GOOS` to `linux` ensures that the compiled executable is compatible with the Go runtime, even if you compile it in a non-Linux environment.

### Windows
**Creating a deployment package on Windows:**   
To create a .zip file archive that works on Lambda using Windows, we recommend installing the build-lambda-zip tool.
To download the `build-lambda-zip` tool, run the following command:
```shell
go.exe get -u github.com/aws/aws-lambda-go/cmd/build-lambda-zip
```
Use the tool from your GOPATH. If you have a default installation of Go, the tool is typically in `%USERPROFILE%\Go\bin`.
Otherwise, navigate to where you installed the Go runtime and do one of the following:

In cmd.exe, run the following:
```shell
set GOOS=linux
go build -o main
%USERPROFILE%\Go\bin\build-lambda-zip.exe -output _lambda.zip main
