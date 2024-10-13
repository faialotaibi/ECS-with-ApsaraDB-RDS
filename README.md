# ECS-with-ApsaraDB-RDS


## Network Setup

- Create VPC with 2 vSwitches
<img width="1680" alt="Screen Shot 1446-04-09 at 6 42 53 PM" src="https://github.com/user-attachments/assets/d0dd63f3-3fab-409d-bbcb-501f53187002">

<img width="1680" alt="Screen Shot 1446-04-09 at 6 43 11 PM" src="https://github.com/user-attachments/assets/5da85219-c5b5-4dc9-bdda-c6f8095bbd56">

- Create Security Group for ECS

<img width="1680" alt="Screen Shot 1446-04-10 at 2 41 20 PM" src="https://github.com/user-attachments/assets/94724070-516b-4a5d-9b12-963e3903af98">

  
<img width="1680" alt="Screen Shot 1446-04-09 at 6 47 43 PM" src="https://github.com/user-attachments/assets/1e35627a-19aa-498f-9754-b5fa67c72949">


## Server Setup

- Create SSH Key Pair
<img width="1680" alt="Screen Shot 1446-04-09 at 6 49 23 PM" src="https://github.com/user-attachments/assets/135d7ded-42ae-4c3e-9362-7117851588b6">

- Create Elastic Compute Service (ECS)

<img width="1675" alt="Screen Shot 1446-04-10 at 2 46 51 PM" src="https://github.com/user-attachments/assets/e12e6026-0713-4929-bfdb-125ed27d913d">

<img width="1680" alt="Screen Shot 1446-04-09 at 6 50 34 PM" src="https://github.com/user-attachments/assets/75bc2385-d140-4216-8e10-7e0717b31add">

<img width="1680" alt="Screen Shot 1446-04-09 at 6 51 16 PM" src="https://github.com/user-attachments/assets/ddb0311c-9d1b-40b2-a632-c60ee5cbceb3">

<img width="1680" alt="Screen Shot 1446-04-09 at 6 52 48 PM" src="https://github.com/user-attachments/assets/1ab52398-7a61-49e5-bc75-b1570cea1ee7">

<img width="1680" alt="Screen Shot 1446-04-09 at 6 53 37 PM" src="https://github.com/user-attachments/assets/03308f97-a2e8-4c4b-a2ac-83c4f6432fd0">

<img width="1680" alt="Screen Shot 1446-04-09 at 6 54 12 PM" src="https://github.com/user-attachments/assets/93491ee2-4b27-42cc-b2d0-20c3dbc09e6d">

## Database Setup

- Create ApsaraDB RDS MySQL Database

<img width="1680" alt="Screen Shot 1446-04-09 at 6 59 04 PM" src="https://github.com/user-attachments/assets/5620abad-994a-493e-961a-d66b63ae95d4">

<img width="1680" alt="Screen Shot 1446-04-09 at 7 00 06 PM" src="https://github.com/user-attachments/assets/d596c423-46b0-4e5b-93b6-d11586ed1a8f">

<img width="1680" alt="Screen Shot 1446-04-09 at 7 00 46 PM" src="https://github.com/user-attachments/assets/ab11a6f9-7079-4b1c-b400-85d9c8fa3656">

<img width="1680" alt="Screen Shot 1446-04-09 at 7 02 49 PM" src="https://github.com/user-attachments/assets/464441b2-6ccb-44f5-ab37-990acc65d65b">

<img width="1680" alt="Screen Shot 1446-04-09 at 7 04 09 PM" src="https://github.com/user-attachments/assets/e2a2677f-91b2-4af2-a6be-13b3ae93b2e1">

- Create Database Security Group, Allowing Inbound through port 3306 From ESC Only

<img width="1680" alt="Screen Shot 1446-04-09 at 7 13 45 PM" src="https://github.com/user-attachments/assets/05b75eb1-38a9-4ca2-a345-8313074bd568">

- Go to Database and add the security group
<img width="1680" alt="Screen Shot 1446-04-10 at 3 00 45 PM" src="https://github.com/user-attachments/assets/24839b91-d068-4123-9a5e-5b68a4038c81">

<img width="1680" alt="Screen Shot 1446-04-10 at 3 02 44 PM" src="https://github.com/user-attachments/assets/f7be2010-4c1d-4c2a-9561-16ff5bf0c854">


- Create Database Account

<img width="1679" alt="Screen Shot 1446-04-10 at 3 13 15 PM" src="https://github.com/user-attachments/assets/5e78638d-a1c6-41e3-ab6a-7b1122fdef9b">

<img width="1680" alt="Screen Shot 1446-04-10 at 3 15 20 PM" src="https://github.com/user-attachments/assets/b9bc15ed-0798-434f-a477-7fefdc87b009">



## Application Setup

- SSH to Sever via Commandline

```
ssh -i ecs.pem root@public-ip
```

- Download php and mysql

```
apt update
apt install php php-mysqli
```

- Verify php

```
php -v
```

- Open application code file

```
nano /var/www/html/db_connection_test.php
```

- Write application that checks Database connection
```
<?php
$db_host = 'db-host';      // db internal endpoint
$db_user = 'myapp';    // your db user account
$db_pass = 'My_password';  // your db password
$db_name = 'myappdb';      // your db name

// create connection
$conn = new mysqli($db_host, $db_user, $db_pass, $db_name);

// check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully";
?>
```


## Check application via Browser

- Co to `http://ecs-public-ip/db_connection_test.php`
<img width="1680" alt="Screen Shot 1446-04-09 at 7 49 25 PM" src="https://github.com/user-attachments/assets/d80021a9-852f-4070-9bc3-1cc2825f4322">

