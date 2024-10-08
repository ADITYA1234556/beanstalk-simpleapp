# This is more of a test code to play with AWS elasticbeanstalk using AWS Codepipeline

CodePipeline can trigger the pipe during
1. Events = Preferred way, to start the pipeline on a new event like push will trigger the codepipeline.
2. Webhooks = Older way, Codepipe will expose a HTTPS endpoint and that will be triggered by a script that will send a payload to codepipeline when an event occurs and that will trigger the pipeline.
3. Polling = Regular checks from codepipeline to github like cron jobs but not as efficient as previous methods.

## CodePipeline Best Practices
1. One code pipeline
2. One code deploy
3. Deploy it to multiple environments or deployment groups in parallel
4. Parallel actions using RunOrder can also speed things up by having one code commit and two code build actions
5. We can deploy to one environment check the status of the changes ifeveryhing is good we can set up a manual approve, once approved it will continue deploying it to prod environment.

## CodePipeline and EventBridge
1. Eventbridge can detect and react to changes in executiont states like intercept failures at certaing stages and then invoke a lambda function. For e.g. Diagnose the code or send SNS notify to a user.
2. **Lambda** There is no way for now to invoke a REST API from codepipeline so we can extend its capability to invoke lambda function which will in turn call a REST API.

## CodePipeline - MultiRegion
1. Say we have a CodePipeline in eu-west-2 so we will have a S3 bucket with artifacts in the same region.
2. Now CodeBuild will build the code and return a cloudformation template in YAML format to deploy the lambda function
3. In our second region us-east-2 we should have a S3 bucket to store artifact, now codepipleine will send the artifcat from eu-west-2 to us-east-2 automatically and cloudformation will invoke the lamda function to deploy the app.
