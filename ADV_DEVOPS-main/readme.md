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

//
https://drive.google.com/drive/folders/1KNzz2insrYhjL3P67V6nhFfgaiE6NAiZ

escape , shift colon , wq then enter

sudo apt --fix-broken install
sudo apt update

sudo apt install build-essential

public class Main {
    public static void main(String[] args) {
        System.out.print("heloo guys");
    }
}


#include<iostream>
using namespace std;

int main(){
    cout << "hellooo";
    return 0;
}

//
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi

please run in elevated terminal
like powershell with administrator rights
//

provider "aws" {
  region = "ap-southeast-2"
}

resource "aws_instance" "exam" {
  ami           = "ami-0df4b2961410d4cff"
  instance_type = "t2.micro"
  tags = {
    "Name" : "exam-aws"
  }
}
//


AWS S3 File Upload + Lambda Trigger
https://www.youtube.com/watch?v=OJrxbr9ebDE
