# AWS


![DevOps - Cloud.jpg](src/img/DevOps%20-%20Cloud.jpg)

AWS kaynaklarının standart adres yolları

ARN

```
arn:aws:resource-groups:us-east-1:1111111:group/Arge_Departmani_Kaynaklari

arn:aws:account        :          :1111111:account

arn:aws:iam:           :1111111:user/AbdussamedBey
```

AWS Management Console Giriş Adresleri

AWS_ID_NUMARAN : 1111 2222 3333

https://111122223333.signin.aws.amazon.com/console

---
AWS ID yerine oluşturduğun bir FIRMA ADI ile giriş adresi
FIRMA ADI : MurlindaSoft

https://MurlindaSoft.signin.aws.amazon.com/console

---
Parola kuralımız

1 büyük harf

1 küçük harf

1 sayı

1 simge

```
Adana_01
Ankara_06
Antalya_07
Izmir_35
Istanbul_34
Trabzon_61
Agri_004
```
---

---
Amazon CLI - Setup

https://aws.amazon.com/cli/

---
AWS CLI Command Reference

https://docs.aws.amazon.com/cli/latest/

---

Termimalden AWS'ye erişmek için Access key oluşturacağız.

Kullanıcı adı ->  Security credentials -> Create access key

Adres burası
https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#security_credential

---

Access key
AAAAAAAAAAA

Secret access key
BBBBBBBBBBBB

---
Terminali aç.

```
aws --version
```
```
aws configure
```
```
AWS Access Key ID [****************]: AAAAAAAAAAAAA
AWS Secret Access Key [****************]: BBBBBBBBB
Default region name [us-east-1]: us-east-1
Default output format [None]: json
```

```
aws ec2 describe-instances
```

---

PuTTY
https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
