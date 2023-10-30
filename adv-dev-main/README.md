# adv-dev
LAMBDA FUNCTION IN S3
(make sure to keep region same for  bucket and lamda)
Search -> S3 BUCKET ->create bucket (do specify AWS region)

Search->lambda -> create function( do specify python, give access permission { i.e change default execution role ->create a new from AWS policy ->give name ->Policy templates – optional->Amazon S3 object read-only permissions } ) -> Add trigger (search s3, choose your bucket ,event=post , add) -> will se trigger created ->go in code and modify it from above -> now test ke side mai click arrow -> go to configure (give name, instead of hello-world select s3 put ,save) -> deploy ->test 
Now go in s3 bucket and upload csv file
Now back to lambda trigger page ->code ke baju mai Monitor section -> go in that -> click on cloud watch -> u can see stream mai csv ka data -> done (remember to delete all instances)



Code 
import json
import boto3
import csv
import io
s3Client = boto3.client('s3')
def lambda_handler(event, context):
   print(event)
   bucket = event['Record'][0]['s3']['bucket']['name']
   key=event['Record'][0]['s3']['object']['key']
   print(bucket)
   print(key)
   #Get our object
   response - s3Client.get_object(Bucket=bucket, Key=key)
   #process it
   data=response['Body'].read().decode('utf-8')
   reader=csv.reader(io.StringIO(data))
   next(reader)
   for row in reader:
       print(str.format("Year - {},Mileage - {},price-{}",row[0],row[1],row[2]))




DYNAMO DB
Search dynamodb-> create table (name) 
Search IMA -> go to roles -> create role ->use case (select Lambda) -> then permission policie -> search this AmazonDynamoDBFullAccess ->next-> role name -> create role

Search lambda -> create function ->name -> runtime(python) ->Change default execution role -> select already exist -> select existing one ->create function ->go to code(paste code) -> now test ke side mai click arrow -> go to configure (give name, chande key value to { {  "id": 35,  "name": "mamta",  "surname": "gupta"}} ,save) -> deploy ->test 




Code 
#importing packages 
import json 
import boto3 
#function definition 
def lambda_handler(event,context): 
	dynamodb = boto3.resource('dynamodb') 
	#table name 
	table = dynamodb.Table('sample') 
	#inserting values into table 
	response = table.put_item( 
	Item={ 
			'sample': 'bhagi', 
			} 
	) 
	return response










PIPELINE
	
AWSCodeCommitPowerUser
IAMSelfManageServiceSpecificCredentials
IAMReadOnlyAccess
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<Bucket_name>/*"
        }
    ]
}
