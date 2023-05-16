*TASK-9: Static website with S3 and CloudFront #63*

U tasku 9 je zadatak napraviti .html file koji ce prikazivati Vaše ime i prezime, kratki Vaš opis, te DevOps image koji koristimo od početka programa. HTML file uredite kako god želite (text, colors, fonts, etc.), nije bitno, ali da je preglednost u najmanju ruku okey.

Potrebno je kreirati S3 bucket u formatu: ime-prezime-devops-mentorship-program-week-11, te omogućiti static website:

Dodati .html i error.html file,
Podesiti bucket na public access, te dodati bucket policy koji će omogućiti samo minimalne access permissions nad bucketom.
Drugi dio zadatka jeste objaviti tu statičku web stranicu kroz CloudFront distribuciju.

Koraci za izradu zadatka:
1. Kreirati .html file i error.html file 

2. Kreirati bucket 
- Bucket name - ime-prezime-devops-mentorship-program-week-11

- AWS Region - izaberete region u kojem zelite kreirati S3 bucket - eu-east-1

- Object ownership - ostaviti kako jeste ALS disabled

- Block all public access - odstrihirati kako bi bucket bio public i u warning prompt-u kliknuti na I acknowledge ...

- Bucket versioning - ostaviti Disable

- Create bucket

![1 bucketcreated](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/db462d1b-d938-4b44-ae05-a574a41bf277)

3. Dodati file-ove na kreirani bucket - Upload 

![2 addedfiles](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/9c1ca0db-4527-4161-a239-c425fff3cbfc)


4. Properties -> Static website hosting -> Enable

![4 staticwebsitehosting](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/f67ae011-85d1-46fa-ba24-9ed3325497be)


5. Permissions -> Public access -> Dodati bucket policy 
![3 bucketpolicy](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/b8b2e5ea-48e6-48ad-b768-041d977b6429)

http://alma-drina-devops-mentorship-program-week-11.s3-website-us-east-1.amazonaws.com

![5 mywebsite](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/da8d682c-17ed-4987-86bc-ebe33cbcbd0b)

6. Kreiranje SSL certifikata u AWS Certificate Manager-a
![7 sslcertificate](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/c48b0060-dc6e-422e-bb70-d6fe11e46402)


7. Kreiranje Cloud Front distrubucije

Create Cloud Front distribution

Origin domain - izaberemo s3 bucket

Origin path preskocimo

Name ostavimo defaultno

Origin access - public

Default root object - index.html

Viewer protocol policy- (Redirect HTTP to HTTPS)

Settings - Custom SSL certificate - izaberemo kreirani Amazon certifikat

![7 sslcertificate](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/ed0bca10-d03c-4886-aff4-e6452e73f528)


![6 cloudfront](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/17feb740-d671-47a4-a437-476c57afb366)

8. Konfigurišemo Route 53 kroz CLI
# Route 53 configuration:
`aws route53 change-resource-record-sets --hosted-zone-id Z3LHP8UIUC8CDK --change-batch '{"Changes":[{"Action":"CREATE","ResourceRecordSet":{"Name":"www.alma-drina.awsbosnia.com","Type":"CNAME","TTL":60,"ResourceRecords":[{"Value":"dv97pz9qp7uan.cloudfront.net"}]}}]}'` 

9. R53 record - encrypted

![8 mywebsitedomain](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/04527eb9-df8d-4d88-88c4-f7a33fdb3a2f)












