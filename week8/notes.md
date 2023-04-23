1.	KREIRAMO EC2 instancu
2.	 Spojimo se na EC2 instancu $ ssh -i "kljuc.pem" ec2-user@ip-adresa
3.	Instaliramo nginx na sljedeći način: 
$ sudo su -
$ yum install nginx -y
$ systemctl start nginx
$ systemctl enable nginx


![1](https://user-images.githubusercontent.com/72069598/233850915-3a477fc5-2996-4a6b-b789-2565d38aefd9.png)

**Kreiranje AMI image od postojece instance:**

![2](https://user-images.githubusercontent.com/72069598/233851003-0592a20d-3750-4d5f-b1d8-988d203be790.png)


Terminiramo instancu ali AMI image nastavlja da živi, te od njega pravimo novu instancu.

**Kreiranje novih instanci od AMI image-a**

![3](https://user-images.githubusercontent.com/72069598/233851047-21020a9f-b04f-4c04-b504-bfa2b82ef904.png)


**Kreiramo minimalno 2 EC2 instance kako bismo napravili ALB – Application Load Balancer**


![4](https://user-images.githubusercontent.com/72069598/233851114-25a8d42f-9489-4353-ba6f-570d86ae5412.png)


**Kreiranje Target group: **

![5](https://user-images.githubusercontent.com/72069598/233851171-a9d9ba88-e35e-49a6-a44c-d9acadf1079f.png)

Od sada nas ALB ima DNS name i EC2 instancama vise ne pristupamo preko njihovih Public IP adresa, vec preko DNS name ALB

*Welcome to nginx! (alb-web-servers-2118216211.us-east-1.elb.amazonaws.com)*


**Kreiranje Autoscaling group**

![7](https://user-images.githubusercontent.com/72069598/233851343-cfe63c4f-147d-4c78-a54a-5396a585621a.png)

![8](https://user-images.githubusercontent.com/72069598/233851324-005defe8-f607-494e-9ce1-58e864aa8632.png)


•	Desired capacity - postavimo zeljeni broj EC2 instanci koji mora biti u opsegu min <= desired < max - 3

•	Minimum capacity- 2

•	Maximum capacity - 4

![9](https://user-images.githubusercontent.com/72069598/233851447-bae0c872-da3d-4d2f-bd0d-90534a1eae1c.png)

![10](https://user-images.githubusercontent.com/72069598/233851463-1e1835e5-4007-4567-b92a-0a1d345594a5.png)


*Stress test: *
sudo yum install stress –y

sudo stress --cpu 8 --vm-bytes $(awk '/MemAvailable/{printf "%d\n", $2 * 0.9;}' < /proc/meminfo)k --vm-keep -m 1


![11](https://user-images.githubusercontent.com/72069598/233851527-611b8a59-cca3-40d3-aa0d-aa5512359669.png)




