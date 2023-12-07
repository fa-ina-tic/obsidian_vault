1. sample training 로컬에서 진행
	1. Lakectl로 레포에 로컬 데이터 업로드 해보고,
	2. 해당 레포 로컬로 클론해서 사용 되는 지 확인
2. 서버에서 GPU 사용한 training 진행
	1. Data Loader 코드 적고
	2. 학습환경 도커로 만든다음에
	3. 학습 뾰로롱 돌려보기 -> s3 compatible api 제공 확인했습니다:) 그냥 간단하게 data loader로 사용 가능하겠군요~:)


uri format: _lakefs://{repo_name}/{branch_name}/{dir}_
python sdk : pip install lakefs
> requirements : Python 3.9+



## CLI(lakectl 활용법)

1. branch 생성
~~~bash
lakectl branch create {New Branch} --source {Srouce Branch}
~~~
1. repo로 로컬 데이터 업로드
~~~bash
lakectl fs upload {path} --source {file_dir} --recursive
\\ equivalant to git add
~~~
~~~bash
lakectl fs commit {path} --message {Commit Message}
\\ commit changes. uncommit changes would be deleted due to Garbage Collection [Document link](https://docs.lakefs.io/howto/garbage-collection/gc.html)
~~~
1. local로 Repo에 있는 파일 다운로드
~~~bash
lakectl fs download {Path URI} [{Destination Path}] --recursive
~~~

## Python SDK
[Document](https://pydocs-lakefs.lakefs.io/index.html)

Python Dataload -> boto3 쓰면 됩니다.
s3 compatible api를 expose하기 때문에, 그대로 사용하면 됩니다.
_example code_
~~~python
import boto3
s3 = boto3.client('s3',
    endpoint_url='https://lakefs.example.com',
    aws_access_key_id='AKIAIOSFODNN7EXAMPLE',
    aws_secret_access_key='wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY')

## put an object into lakefs
with open('/local/path/to/file_0', 'rb') as f:
    s3.put_object(Body=f, Bucket='example-repo', Key='main/example-file.parquet')

## list object
list_resp = s3.list_objects_v2(Bucket='example-repo', Prefix='main/example-prefix')
for obj in list_resp['Contents']:
    print(obj['Key'])

## get object metadata
s3.head_object(Bucket='example-repo', Key='main/example-file.parquet')
# output:
# {'ResponseMetadata': {'RequestId': '72A9EBD1210E90FA',
#  'HostId': '',
#  'HTTPStatusCode': 200,
#  'HTTPHeaders': {'accept-ranges': 'bytes',
#   'content-length': '1024',
#   'etag': '"2398bc5880e535c61f7624ad6f138d62"',
#   'last-modified': 'Sun, 24 May 2020 10:42:24 GMT',
#   'x-amz-request-id': '72A9EBD1210E90FA',
#   'date': 'Sun, 24 May 2020 10:45:42 GMT'},
#  'RetryAttempts': 0},
# 'AcceptRanges': 'bytes',
# 'LastModified': datetime.datetime(2020, 5, 24, 10, 42, 24, tzinfo=tzutc()),
# 'ContentLength': 1024,
# 'ETag': '"2398bc5880e535c61f7624ad6f138d62"',
# 'Metadata': {}}

~~~

## issue
branch protection lakectl로 안됨 -> gui상에서는 가능
