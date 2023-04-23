1.	KREIRAMO EC2 instancu
2.	 Spojimo se na EC2 instancu $ ssh -i "kljuc.pem" ec2-user@ip-adresa
3.	Instaliramo nginx na sljedeći način: 
$ sudo su -
$ yum install nginx -y
$ systemctl start nginx
$ systemctl enable nginx

image.png
