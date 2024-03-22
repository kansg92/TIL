AWS-ses

# AWS SES(Simple Email Service)

클라우드 기반 이메일 발송 서비스이며 안전하고 확장 가능한 방식으로 이메을 보낼 수 있다.

## SES  제공 기능

1. **이메일 발송**: SES를 사용하여 전자 메일을 안전하게 발송할 수 있습니다. 이메일은 SMTP(간단한 메일 전송 프로토콜) 또는 SES API를 통해 발송할 수 있습니다.
2. **템플릿과 변수**: SES는 이메일 발송을 위한 템플릿을 지원하며, 동적으로 데이터를 삽입할 수 있는 변수를 제공합니다. 이를 통해 개인화된 이메일을 보낼 수 있습니다.
3. **발송 제한 관리**: SES는 이메일 발송량을 제한하고 모니터링할 수 있는 기능을 제공합니다. 이를 통해 사용량을 관리하고 비용을 절감할 수 있습니다.
4. **반송 관리**: SES는 반송된 이메일을 자동으로 처리하고 관리할 수 있습니다. 이를 통해 이메일 전송 문제를 식별하고 해결할 수 있습니다.
5. **스팸 필터링**: SES는 스팸 필터링 기능을 제공하여 전송된 이메일이 수신자의 스팸함으로 이동하는 것을 방지합니다.

## 기본 셋팅

1. 전송용 IAM계정을 맏든다.

2. SES Fullaccess 권한을 할당한다.

   ```python
   AmazoneSesSendingAccess
   
   {
   "Version": "2012-10-17",
   "Statement": [
   {
   "Effect": "Allow",
   "Action": "ses:SendRawEmail",
   "Resource": "*"
   }
   ]
   }
   ```

3. … 추후 작성

4. AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY 가필요!!!

## python sample code

```python
import boto3
import os
from botocore.exceptions import ClientError

os.environ["AWS_ACCESS_KEY_ID"] = "AWS_ACCESS_KEY_ID"
os.environ["AWS_SECRET_ACCESS_KEY"] = "AWS_SECRET_ACCESS_KEY"
os.environ["AWS_DEFAULT_REGION"] = 'ap-northeast-2'

def template(payload):
  
  with open('./template/test.html', 'r', encoding='utf-8') as file:
    html_template = file.read()
  return html_template.format(user=payload['user'],pdf_url=payload['pdf_url'])
  
  

def send_email_aws(sender_email, recipient_email, subject, body_html):
  # AWS SES 클라이언트 생성
  ses_client = boto3.client('ses')

  # 이메일 구성
  email_message = {
      'Subject': {'Data': subject},
      'Body': {
          'Text': {'Data': '안녕하세요, REER서비스입니다. 예산서가 도착했습니다. 예산서를 확인해주세요'},
          'Html': {'Data': body_html}
      }
  }

  try:
      # 이메일 발송 요청
      response = ses_client.send_email(
          Source=sender_email,
          Destination={'ToAddresses': [recipient_email]},
          Message=email_message
      )
  except ClientError as e:
      print("이메일 발송 실패:", e.response['Error']['Message'])
  else:
      print("이메일이 성공적으로 발송되었습니다.")
      print("Message ID:", response['MessageId'])

# 이메일 발송에 사용할 정보
payload = {'user':'김고객', 'pdf_url' : '#'}
sender_email = 'test@zero-to-n.com'
recipient_email = 'kansg922@gmail.com'
subject = '[REER] 리모델링 예산서가 도착했습니다.'
body_text = '안녕하세요, REER서비스입니다. 본 글이 나오면 사이트에 문의해주세요.'
body_html = template(payload)

# 이메일 발송 함수 호출
send_email_aws(sender_email, recipient_email, subject, body_html)
```