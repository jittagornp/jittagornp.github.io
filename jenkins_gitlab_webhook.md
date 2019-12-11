# Jenkins + GitLab Webhook

# ที่ Jenkins 
### 1. Generate API Token 
- ไปที่ข้อมูล User Login 
- จำ User ID เอาไว้ => (`JENKINS_USER_ID`)
- ไปที่เมนู Configure
- Add new Token => (`JENKINS_USER_TOKEN`)
- Copy Token นั้นเก็บไว้ 

### 2. Add Authenticity Token 
- ไปยัง Job ที่ต้องการทำ Webhook => (`JOB_NAME`)
- ไปที่เมนู Configure
- ไปที่ส่วน Build Triggers 
- ติ๊กถูก `Trigger builds remotely (e.g., from scripts)`  
- Set `Authentication Token` เข้าไป => (`AUTHENTICITY_TOKEN`)

# ที่ GitLab 
### 3. ผูก WebHook 
- ไปยัง Project ที่ต้องการทำ Webhook
- ไปที่เมนู Settings > Integrations 
- วาง URL ดังต่อไปนี้ลงไป

format  
> https://`<JENKINS_USER_ID>`:`<JENKINS_USER_TOKEN>`@/job/`<JOB_NAME>`/build?token=`<AUTHENTICITY_TOKEN>`

ตัวอย่าง  
> https://hunter:11a403302a4f01b9b4975c0ac27441a5cc@/job/construction/build?token=Aju9ryHUu6t7W8wLSeCWtY2bWjzQduYNPyY7B3gs

- ติ๊ก `Push envents` 
- set `This URL will be triggered by a push to the repository` เป็น master
- คลิกที่ปุ่ม `Add webhook`

ลอง test ดู  
