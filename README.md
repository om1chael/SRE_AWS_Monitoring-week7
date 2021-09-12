
AWS Model Overivew:

![image](https://user-images.githubusercontent.com/88166874/132838647-78873ea4-51c1-410a-95cf-8bc5ca1cc5f7.png)

# Goals:
The goal of this repo is to to add Auto Scaling And Load Balancing to your system. 

 - Required Tasks:
    -Creating a Launch Template
    - Create Auto Scaling Group
        - add a Load Balancer
    - Target Group Configuration
    - Testing the scaling  


# Creating a Launch Template 
### Cretaing an image  defines the instnaces that you want to create more of when you scale. 


![image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2019/11/25/Instance-type-example.png)
   

1. Press on the instance you want to auto-scale:
    - Then select `Actions` -> `Images and templates` -> `Create template from instance`. 

you should be met with this page. 
![image](https://www.hava.io/hs-fs/hubfs/AWS%20Ec2%20Autoscaling%203.png?width=1488&name=AWS%20Ec2%20Autoscaling%203.png)


2. Most of the rest of the details will be automatically filled in.

3. In Network settings, Select the VPC, then select the security group (Making sure its the same group as your instance )
4. skip advanced and click `Create launch template`
___
## Create Auto Scaling Group With Load Balancer :

1. On the launch template confirmation page, click Create Auto Scaling Group.
2. Give the scaling group a name
3. Skip `Launch Template` and leave `Instance purchase options` as `Adhere to launch template.` 
5. In Network, select the subnet that your instance is operating in (public, in our case), then click `Next`

# Adding the Load Balancer

6. Attach to a new load balancer, setting the type to 
Application load balancer. 

![image](https://application-migration-with-aws.workshop.aws/ecs/create-lb.png)

7. Name it The loadbalancer and set it as Internet-facing

8. In Listeners and routing, select Create a target group. Tick the box for ELB, and Enable group metrics collection within CloudWatch.
9. Configure the settings like this:
```
    - Desired capacity: 1
    - Minimum capacity: 1
    - Maximum capacity: 3.
    - Scaling policies: Target tracking scaling policy
    - Metric type: CPU
    - Target value: 50 (The threshold of the CPU)
```

10. `Create auto scaling group`

___
## Looking at your Autoscaling group:

1. In the EC2 tab, scroll down till you see `AUTO SCALING ` then click on the `Auto Scaling Groups`
2. This page should load all the scaling groups that have been configured. 
3. Press on your scaling groups and click on the `automatic scaling group ` option

# Testing:
Try pushing your EC2 instance to above 50%. If this is true, then a new instance will be cerated. 
