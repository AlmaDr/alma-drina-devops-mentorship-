# Branching Models

•	Imamo dva popularna branching modela koje klijenti implementiraju u svojim organizacijama. Jedan je *Trunk Based model* dok je drugi *Feature-based ili GitFlow model.
Trunk-based development*

•	Unutar **Trunk-based modela**, developeri suradjuju unutar jednog branch-a ili trunk-a izbjegavajući kompleksnost merganja. Ovaj model je preporucen timovima unutar Amazona i praksa je da se radi Continuous Integration gdje developeri rade marganje nekoliko puta u toku dana na centralni repozitorij. 

**Feature-based aka GitFlow development**

•	Razlozi zasto se koristi ovaj model:

- zato što vise timova moze raditi na razlicitim feature release-ima sa razlicitim timeline-ima. 
- organizacije koje pruzaju SAAS (Software As-A Service) mozda imaju klijente koji ne zele biti na posljednjim verzijama sve vrijeme te je neophodno da kreiraju nekoliko "Release" i "Hotfix" brancheva.
- Neki timovi mozda imaju specificne QA zahtjeve - primjer manual approval sto dovodi do kašnjenja obzirom da su neki featuri predstavljeni prije produkcije


**GitFlow**


•	Ukljucuje nekoliko level-a branching-a sa master grane gdje promjene na feature branches su samo periodicno merge-ane na master granu i gdje trigger-uju release.

•	U ovom slucaju Master grana uvijek sadrzi produkcijski kod.

•	Develop grana sadrzi novi development kod.

•	Ove dvije grane su tzv. long-running branches - one ostaju u nasim projektima sve vrijeme, dok druge grane, za neke features ili releases, postoje samo privremeno - kreiraju se po potrebi i uklonjene su nakon sto su ispunile svoju svrhu.

# KREIRANJE WORKSPACE-a

***AWS CLOUD9*** - je servis koji omogućava da se piše i pokreće kod kroz browser.
Koraci za kreiranje workspace-a su sljedeći:
1. Prijavimo se na naš AWS kao IAM user
2. Kroz konzolu Cloud9 odaberemo **Create environment**
3. Imenujemo ga kao **gitflow-workshop** dok ostali podaci ostaju po defaultu
4. Kada se kreira environment, mozemo zatvoriti welcome tab i lower work area i otvoriti terminal.

![1  gitflow-worshop](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/eebaf3d2-f681-4e28-8393-edcac651397d)

Po defaultu Amazon EBS koji se nalazi na Cloud9 instanci je 10 GiB. Da bismo pto provjerili koristimo komandu 
`$ df -h`

Nakon toga kreiramo file resize.sh putem komande koja se može pronaći ovdje https://catalog.us-east-1.prod.workshops.aws/workshops/484a7839-1887-43e8-a541-a8c014cd5b18/en-US/introduction/access-cloud9


Nakon čega sljedećom komandom mijenjamo veličinu attachovanog EBS-a na 30 GiB

`$ bash resize.sh 30`


![2  resizesh](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/fd93e646-fa5b-4e0d-8af0-2e989912402b)

# Initial Setup

Nakon što smo promijenili veličinu EBS-a potrebno je da uradimo inicijalni setup koristeci komandu `$git config` gdje cemo unijeti naše podatke: git user.name i git user.email:

`$ git config --global user.name "alma-drina"`

`$ git config --global user.email alma-ka@hotmail.com
`

U terminalu je potrebno unijeti sljedeće komande kako bismo konfigurisali AWS CLI helper za HTTPS konekciju:
```
$ git config --global credential.helper '!aws codecommit credential-helper $@'
$ git config --global credential.UseHttpPath true
```


Da bismo pokrenuli gitflow, potrebno je da ga instaliramo: 
```
$ curl -OL https://raw.github.com/nvie/gitflow/develop/contrib/gitflow-installer.sh
$ chmod +x gitflow-installer.sh
$ sudo git config --global url."https://github.com".insteadOf git://github.com
$ sudo ./gitflow-installer.sh
```


![3  gitflow](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/92433976-45cf-4577-b378-598ba744eb8c)

# AWS CloudFormation


![4  gitflowformation](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/950271ce-eee5-476b-9604-0c93760df5ff)


•	U ovom modulu koristit ćemo AWS CloudFormation kako bismo postavili aplikaciju i infrastrukturu koja joj pripada. Iskoristiti cemo i AWS Elastic Beanstalk kako bismo pojednostavili porces.

# Master Branch

**Elastic Beanstalk

•	Kako bismo pojednostavili proces podesavanja i konfigurisanja EC2 instanci,koristit ćemo nodejs environment koristeci AWS Elastic Beanstalk - koji ce dopustiti da lako hostujemo web aplikacije bez potrebe da lansiramo, konfigurisemo ili operiramo virtuelnim serverima na svoju ruku. Automatski provizionira i operira infrastrukturom (primjer virtuelnim serverima, load balancerima itd.) i provide-a aplikacijski stack (primjer operativni sistem, programski jezik i framework, web i aplikacijski server itd.) za nas.

**STAGE 1 - KREIRATI CODE COMMIT REPOZITORIJ**

•	U ovom koraku cemo napraviti kopiju aplikacijskog koda i kreirati ` $ code commit` repozitorij koji ce hostovati nas kod.

`$ aws codecommit create-repository --repository-name gitflow-workshop --repository-description "Repository for Gitflow Workshop"`

`$ git clone https://git-codecommit.us-east-1.amazonaws.com/v1/repos/gitflow-workshop`

![5  codecommit](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/4ca8ad26-a41d-4a73-a31e-c95603999615)

**STAGE 2 - DOWNLOAD THE SAMPLE CODE AND COMMIT YOUR CODE TO THE REPOSITORY**

1. Preuzeti Simple app:
`$ ASSETURL="https://static.us-east-1.prod.workshops.aws/public/442d5fda-58ca-41f0-9fbe-558b6ff4c71a/assets/workshop-assets.zip"; wget -O gitflow.zip "$ASSETURL"`
2. A zatim: 
`$ unzip gitflow.zip -d gitflow-workshop/`
3. Promijeniti direktorij u nas lokalni repo folder i pokrenuti git add:
`$ cd gitflow-workshop `
`$ git add -A`
4. Pokrenuti komandu `$ git commit` kako bismo komitali promjene i gurnuli ih na ` master` granu
`$ git commit -m "Initial Commit"`
`$ git push origin master`

![6  gitpush](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/52b07f9f-bbee-487c-8a68-7c727cdc4900)



![7  gitcommit](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/e53092eb-4d14-4e51-8511-82efe982af99)




![8  gitpushorigin](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/214ab877-d09e-49e4-b294-4ab7c6204573)


**CREATE ELASTIC BEANSTALK APPLICATION**

*To use Elastic Beanstalk we will first create an application, which represents your web application in AWS. In Elastic Beanstalk an application serves as a container for the environments that run your web app, and versions of your web app's source code, saved configurations, logs, and other artifacts that you create while using Elastic Beanstalk.*

•	Pokrenut ćemo template ispod kako bi kreirali EB application i S3 Bucket za artifakte. Bitna napomena - EB aplikaciju mozemo posmatrati kao folder koji sadrzava komponente naseg Elastic Beanstalk-a dok je S3 bucket za artifakte mjesto gdje cemo postaviti nas aplikacijski code prije deploymenta.

`$ aws cloudformation create-stack --template-body file://appcreate.yaml --stack-name gitflow-eb-app`

•	Kada pokrenemo ovu komandu AWS CloudFormation pocinje kreiranje resursa koji su specificirani u templateu. Nas novi stack gitflow-eb-app se pojavljuje na listi unutar CloudFormation konzole.




![9  cloudformation](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/35aee3f3-4b15-408a-bb44-82db4309ca4a)


•	Nakon toga idemo u Elastic Beanstalk konzolu da viidmo aplikaciju koja je kreirana.

![10  applicationEB](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/7bc2d81e-3a58-4648-81e6-9b9cd65d6698)


# MASTER ENVIRONMENT

•	Sada kreiramo AWS Elastic Beanstalk Master Environment. Mozemo deploy-ati vise okruženja (environments) ako zelimo da pokrenemo vise verzija aplikacije. Naprimjer, mozemo imati development, integracijski i produkcijski environment.
•	Iskoristiti cemo AWS CloudFormation template da set-ujemo elastic beanstalk application i codepipeline da odrade "auto store" nasih artefakata:

`$ aws cloudformation create-stack --template-body file://envcreate.yaml --parameters file://parameters.json --capabilities CAPABILITY_IAM --stack-name gitflow-eb-master`

![12  stack1](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/86e938ae-cf84-4c9e-bcc5-eadec4223402)





![13  applicationEB1](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/1df8e9f3-c7c0-477d-b9cf-3733c14597ca)



![14  envEB](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/7bb351e7-bbe0-43e4-a0ce-40f257a85382)


**AWS CodePipeline

AWS Pipeline je CD servis koji mozemo koristiti da modeliramo, vizualiziramo i automatiziramo korake potrebne da release-amo nas software. Mozemo brzo modelirati i konfigurisati razlicite stadije software release processa. CodePipeline automatizira korake koji su potrebni da se odradi release naseg softvera kontinuirano.
AWS CodePipeline ima akcije: source, build i deploy.



![15  masterpipeline](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/7abea019-0f54-41b1-accd-9f20f60094e9)

•	Primjer deployane nodejs aplikacije kojoj se moze pristupiti preko linka iz AWS Elastic Beanstalk Environment Management Console

![16  masternodejs](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/ae799eb1-e2ba-4a19-b748-e1d1ec4878b9)


# LAMBDA

•	Lambda je compute servis koji nam dopusta da pokrećemo o kod bez provizioniranja ili menadzovanja servera.AWS Lambda pokreće tvoj kod kada je to potrebno, te može biti nekoliko zahtjeva u toku dana ili čak hiljadu u sekundi.PLaćaš koliko koristiš.

**LAMBDA CREATION

`$ aws cloudformation create-stack --template-body file://lambda/lambda-create.yaml --stack-name gitflow-workshop-lambda --capabilities CAPABILITY_IAM`

![18  codecommitlambda](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/c14f6404-bdaa-4d31-b920-aaf154906ca2)

![19  stacklambda](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/52f6e698-6ea9-4000-8981-1d31da8bb1c3)

![20  functionlambda](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/21c0ab1f-3d9d-4b52-9e99-30a39d74d1f0)



**AWS CodeCommit Trigger

1. Otvoriti CodeCommit  console

2. Odabrati gitflow-workshop repositorij gdje je potrebno kreirati trigere za evente

3. Odabrati Settings i zatim Triggers.

4. Create trigger



![21  codecommitrigger](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/49a7abbd-6712-4aa7-b10e-963c729bbcac)


# DEVELOP BRANCH

•	Create Develop branch.
•	Kada koristimo git-flow extension library, pokretanjem git flow init na postojecem repo-u kreiramo develop branch:

```
Admin:~/environment/gitflow-workshop (master) $ git flow init

Which branch should be used for bringing forth production releases?
- master
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
```

![22  developbranch](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/a9fe4771-0da0-44ae-bfc3-256112fec1cc)


*Manuelno kreiran development environment za develop branch*

`$ aws cloudformation create-stack --template-body file://envcreate.yaml --parameters file://parameters-dev.json --capabilities CAPABILITY_IAM --stack-name gitflow-workshop-develop`

![23  developstack](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/db121ea3-4c45-4b00-92f8-c664feb8a581)


![24  masterpipeline](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/1345edcd-d581-4f85-92cb-174e93f9e0b9)


![25  pipelines](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/91201c94-2d5a-4cf0-b8b2-fd8c8cca9ab3)


# Feature Branch
*Each new feature should reside in its own branch, which can be pushed to the central repository for backup/collaboration. But, instead of branching off of master, feature branches use develop as their parent branch. When a feature is complete, it gets merged back into develop. Features should never interact directly with master.

Kreirati Feature Brench:

`$ git flow feature start change-color`

Create feature branch environment
•	Odraditi izmjene vezane za HTML fajl i promjenu boje pozadine.
•	Manuelno trigerovana kreacija of the development environmenta:

`$ aws cloudformation create-stack --template-body file://envcreate.yaml --capabilities CAPABILITY_IAM --stack-name gitflow-workshop-changecolor --parameters ParameterKey=Environment,ParameterValue=gitflow-workshop-changecolor ParameterKey=RepositoryName,ParameterValue=gitflow-workshop ParameterKey=BranchName,ParameterValue=feature/change-color`


![26  futurebranch](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/d3ec42c9-2af6-431b-9e8b-85368b0b4a32)


![27  changecolorstack](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/04deab19-4aba-410f-86ea-86f5e17e34ea)


![28  masterpurple](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/2f5f0c24-42ee-4c70-a360-157d55c5d428)


![29  changecolorgreen](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/afca9529-fe24-4779-a71a-acbd1bbf7d7c)

FEATURE FINISH
•	Kada smo verifikovali izmjene koje smo napravili spremni smo merge-ati u develop granu na sljedeci nacin:
`$ git flow feature finish change-color`
•	a komandom gore smo merge-ali change-color u develop branch, remove-ali smo feature branch i switch-ovali nazad na develop branch.
•	Sada cemo ukloniti feature granu change-color i pushati izmjene remotely istovremeno:
`$ git push origin --delete feature/change-color`


![30  deletefeature](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/0bd62224-0d51-45a5-8c94-551f76183d62)



•	Commitamo develop branch:
`$ git push --set-upstream origin develop`
•	Posljednje izmjene (sa bojom) su vidljive sada na develop branchu:


![31  developgreen](https://github.com/AlmaDr/alma-drina-devops-mentorship-/assets/72069598/28a77f97-8b7c-4c13-8026-09dbb3c995b9)




