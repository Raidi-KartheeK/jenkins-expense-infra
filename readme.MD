**Expense DEV Infrastructure**

![expense-infra](https://github.com/user-attachments/assets/451b4dcc-5031-4a37-a944-8776867fa619)

. Make sure infra is created

. Every resource should have dev in its name so   that it will not overlap with prod resources.

Once infra is setup. We need to configure ingress controller to provide internet access to our expense application.

We are using bastion as our EKS client, so it will have

   .  K9S
   .  kubectl
   .  helm
   .  aws configure

**RDS Configuration**

Since we are using RDS instead of MySQL image, we need to configure RDS manually, we are creating schema as part of RDS but table and user should be created.

Make sure MySQL instance allows port no 3306 from bastion

**mysql -h expense-dev.czn6yzxlcsiv.us-east-1.rds.amazonaws.com -u root -pExpenseApp1**

USE transactions;

CREATE TABLE IF NOT EXISTS transactions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    amount INT,
    description VARCHAR(255)
);

CREATE USER IF NOT EXISTS 'expense'@'%' IDENTIFIED BY 'ExpenseApp@1';

GRANT ALL ON transactions.* TO 'expense'@'%';

FLUSH PRIVILEGES;

 # Target group binding

 If we are running frontend using normal user it can't bind the port 80. non root privelege user running container are not able to open system ports which are under 1024.
So we have to use port no 8080 for frontend. Make sure
nginx.conf opens port no 8080 instead of 80.
ALB target group health check port should be 8080.
frontend service target port should be 8080 instead of 80.