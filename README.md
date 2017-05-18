# CloudFormation
AWS CloudFormation Repository

<p> Description of VPC Template: </p>

<p1> AWS CloudFormation Template for 3 Tier Application VPC:Parameters will define our cloudFormation template. Here we are creating the user option for two VPC CIDR blocks 10.250.0.0 and 10.251.0.0. Mappings: Mappings will map a public and private subnet to our VPC for the webserver and DB isntance Resources: Makes a call to the AWS API with intrinsic fucntions that refer to our parameters e.g Fn::Join. We are defaulting to public DNS and CIDR block /16. We are also mapping our public and private subnets with an intrinsic function Fn::FindInMap referencing our mappings above. Also creating the reources as defined above, RouteTables, InternetGateway, NAT gateways, and Elastic IPs. The Output Section will show the user the reated AWS resources in the AWS cloudFormation GUI </p1>
