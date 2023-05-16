TASK-9: Static website with S3 and CloudFront #63
U tasku 9 je zadatak napraviti .html file koji ce prikazivati Vaše ime i prezime, kratki Vaš opis, te DevOps image koji koristimo od početka programa. HTML file uredite kako god želite (text, colors, fonts, etc.), nije bitno, ali da je preglednost u najmanju ruku okey.

Potrebno je kreirati S3 bucket u formatu: ime-prezime-devops-mentorship-program-week-11, te omogućiti static website:

Dodati .html i error.html file,
Podesiti bucket na public access, te dodati bucket policy koji će omogućiti samo minimalne access permissions nad bucketom.
Drugi dio zadatka jeste objaviti tu statičku web stranicu kroz CloudFront distribuciju.

Koraci za izradu zadatka:
1. Kreirati .html file i error.html file 
2. Kreirati bucket 
Bucket name - ime-prezime-devops-mentorship-program-week-11
AWS Region - izaberete region u kojem zelite kreirati S3 bucket - eu-central-1
Object ownership - ostaviti kako jeste ALS disabled
Block all public access - odstrihirati kako bi bucket bio public i u warning prompt-u kliknuti na I acknowledge ...
Bucket versioning - ostaviti Disable
DODATI TAGOVE
ostalo ostaviti defaultne postavke
Create bucket

3. Dodati file-ove na kreirani bucket - Upload 



4. Properties -> Static website hosting -> Enable

5. Permissions -> Public access -> Dodati bucket policy 

6. Kreiranje SSL certifikata u AWS Certificate Manager-a

7. Kreiranje Cloud Front distrubucije
Create Cloud Front distribution
Origin domain - izaberemo s3 bucket
Origin path preskocimo
Name ostavimo defaultno
Origin access - public
Default root object - index.html
Viewer protocol policy- (Redirect HTTP to HTTPS)
Settings - Custom SSL certificate - izaberemo kreirani Amazon certifikat


8. Konfigurišemo Route 53 kroz CLI
# Route 53 configuration:
`aws route53 change-resource-record-sets --hosted-zone-id Z3LHP8UIUC8CDK --change-batch '{"Changes":[{"Action":"CREATE","ResourceRecordSet":{"Name":"www.alma-drina.awsbosnia.com","Type":"CNAME","TTL":60,"ResourceRecords":[{"Value":"dv97pz9qp7uan.cloudfront.net"}]}}]}'` 

9. Kopiramo domenu u browser www.ime-prezime.awsbosnia.com













