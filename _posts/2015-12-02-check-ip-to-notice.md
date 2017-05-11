---
title: 检查IP是否存在发送邮件提醒
layout: post
date:   2015-12-02 13:31:01 +0800
author: Suuuch
category: Python
tags:
- python
- linux
- postfix
- crontab
---

最近老是忘记打卡，写个Python小脚本给自己提醒下班打开，OA系统也木有接口查看自己实时的打卡状态，
坑爹！！！！！！！


{% highlight python %}
#-*- coding: UTF-8 -*-
import smtplib
from email.MIMEMultipart import MIMEMultipart
from email.MIMEBase import MIMEBase
from email.MIMEText import MIMEText
from email.Utils import COMMASPACE, formatdate
from email import Encoders
import os

def sendMail(to, fro, subject, text, files=[],server="localhost"):
    assert type(to)==list
    assert type(files)==list


    msg = MIMEMultipart()
    msg['From'] = fro
    msg['To'] = COMMASPACE.join(to)
    msg['Date'] = formatdate(localtime=True)
    msg['Subject'] = subject

    msg.attach( MIMEText(text) )

    for file in files:
        part = MIMEBase('application', "octet-stream")
        part.set_payload( open(file,"rb").read() )
        Encoders.encode_base64(part)
        part.add_header('Content-Disposition', 'attachment; filename="%s"'
                       % os.path.basename(file))
        msg.attach(part)

    smtp = smtplib.SMTP(server)
    smtp.sendmail(fro, to, msg.as_string() )
    smtp.close()

# check IP status
import platform
import sys
import time

def get_os():
    '''''
    get os 类型
    '''
    os = platform.system()
    if os == "Windows":
        return "n"
    else:
        return "c"

def ping_ip(ip_str):
    cmd = ["ping", "-{op}".format(op=get_os()),
           "1", ip_str]
    output = os.popen(" ".join(cmd)).readlines()

    flag = False
    for line in list(output):
        if not line:
            continue
        if str(line).upper().find("TTL") >=0:
            flag = True
            break
    return flag

from datetime import datetime
start_time = datetime.now()
#ping_ip('172.20.156.18')
# Example:
send_mail_cnt = 0
while (datetime.now() - start_time).seconds  < 3600:
    if send_mail_cnt >= 3:
        break
    to = ['Suuuch <suuuch@hotmail.com>']
    fro = 'SkyShen <SkyShen@boyaa.com>'
    mail_title = 'Notice!Sign Out!'
    content = 'Notice! Did you sign out?'

    if not ping_ip('172.20.156.18'):
        print ' IP address ( 172.20.156.18) is not alive!Send mail! '
        send_mail_cnt += 1
        sendMail(to,fro,mail_title,content)

    else:
        print 'IP Address is Alive! No Need send mail!'
    time.sleep(300)

{% endhighlight %}
