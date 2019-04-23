# Pipes
A pipeline ..... for managing your pipelines.

The purpose of this project is to manage many CodePipeline's within an organization across multiple accounts. Each pipeline belongs to a Scope that logically separates the permissions of each pipeline. 

# Set up the master pipeline
You will need 3 AWS accounts:
   - cicd
   - dev
   - prod

Within the cicd account, run the Master.template through CloudFormation.
   - Name the stack 'master' or something similar (lowercase).
   - Input Id's for each account
   - Set AllEnvironmentsCreated = False
   - Leave SourceCodeCommitRepo empty
   
Copy down the KmsCmkArn and S3BucketName from the CloudFormation outputs section.
    
With the cicd, dev, and prod accounts, run Master-Environment.template through CloudFormation.
   - Pass in the KmsCmkArn and S3BucketName as parameters
   - Set environment (lowercase)
   - Set AccountId of cicd account
   - Pass in name of master stack (lowercase)

After SDLC stacks have been created, update the master stack within the cicd account.
   - Set AllEnvironmentsCreated = True
   
Copy this repo into the CodeCommit repo created by the master stack.
   - Modify your cfvars/Master.template file with your account ids

# Child Pipelines
Edit your Pipelines.json file as needed. Enjoy!
