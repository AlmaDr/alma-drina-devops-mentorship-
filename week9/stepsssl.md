**TASK-8: Implement SSL Let's Encrypt, migrate to AWS ACM**

- Kreirati DNS record <ime>-<prezime>.awsbosnia.com za Hosted Zone awsbosnia.com (Hosted zone ID: Z3LHP8UIUC8CDK) koji ce da pokazuje na EC2 instancu koju ste krairali. Za kreiranje DNS zapisa korisite AWS CLI AWS kredencijale koji se nalaze unutar sljedeceg excel file-a. AWS CLI konfigurisite tako da koristite named profile aws-bosnia. Kako da podesite AWS CLI i vise o CLI profilima mozete vidjeti ovdje
Za ovaj dio taska mozete da iskorisite change-resource-record-sets AWS CLI komandu. Kada ste dodali novi DNS record njegov Name i Value ispiste uz pomoc komande aws route53 list-hosted-zones i alata jq gdje cete prikazati samo Name i Value za DNS record koji ste vi kreirali odnosno za vase domensko ime.
  
  *Za ispis DNS record Name i Value koristimo sljedeću naredbu:*
  
  `aws route53 list-resource-record-sets --hosted-zone-id Z3LHP8UIUC8CDK | jq '.ResourceRecordSets[] | select(.Name == "ime-prezime.awsbosnia.com.") | {Name, Value}'`
  
  
  ![1  DNS record](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/ff636446-f321-4259-b7b1-0fe11521df07)
  
 -  Na EC2 instanci ec2-ime-prezime-task-8 kreirati Let's Encrypt SSL certifikat za vasu domenu. Neophodno je omoguciti da se nodejs aplikaciji moze pristupiti preko linka https://<ime>-<prezime>.awsbosnia.com, to verifikujte skrinsotom gdje se vidi validan certifikat u browser
  
  
  
  ![2  cert verifikovan](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/4a02a369-e481-489f-9126-4fc39f5208be)
  
  
  
  ![3  dns name https](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/96668e1f-3bb0-4553-91bf-1a319a7e4b77)

  
  •	Koristeci openssl komande prikazati koji SSL certitikat koristite i datum njegovog isteka. 
  
  

![4  expiration date](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/8d9fa83f-0ea4-4597-9d39-a82c4c2e505c)

  
  •	Importujte Lets Encrypt SSL certifikat unutar AWS Certified Managera
  
  ![5  certificate issued](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/9489cb0d-5758-4715-bb8b-c9634d1c049b)


  
  •	Kreirajte Load Balancer gdje cete na nivou Load Balancera da koristite SSL cert koji ste ranije importovali. 
  
  ![6  EC2 -2](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/69593f2d-6438-41a9-a81f-41acf1f7684e)

  
  
  
  ![7  tg 301](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/2cea3194-2e24-4422-9fff-a1f3774d65f7)
  
  
  

  
  ![8  two healty inst](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/d739964a-0b27-4fd6-a989-6b230568935d)

  
  •	Kreirajte novi SSL certifikat unutar AWS Certified Managera, azurirajte ALB da koristi novi SSL cert koji ste kreirali.
  
  ![9  port 80 i 443](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/cd537645-f7fc-48e2-895d-51d684feb4e8)

  ![10](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/6553207f-d053-4d5d-906f-aa3a4ef4d593)

  
  ![11  AMIs](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/cc1bda6a-3cde-4ee7-af74-ee615a2218ed)

  
  
  
