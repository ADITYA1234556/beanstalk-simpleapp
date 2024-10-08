This is more of a test code to play with AWS elasticbeanstalk using AWS Codepipeline

CodePipeline can trigger the pipe during
1. Events = Preferred way, to start the pipeline on a new event like push will trigger the codepipeline.
2. Webhooks = Older way, Codepipe will expose a HTTPS endpoint and that will be triggered by a script that will send a payload to codepipeline when an event occurs and that will trigger the pipeline.
3. Polling = Regular checks from codepipeline to github like cron jobs but not as efficient as previous methods.
