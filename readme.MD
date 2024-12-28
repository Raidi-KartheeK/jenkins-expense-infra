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