## VPC,sub-net_private_public,IGW,NAT ゲートウェイ


```AWSTemplateFormatVersion: 2010-09-09

Resources:
  CfVPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.1.0.0/16
      Tags:
        -
          Key: Name
          Value: CfVPC

  CfPublicSubnet:
    Type: AWS::EC2::Subnet
    Properties:
      CidrBlock: 10.1.1.0/24
      MapPublicIpOnLaunch: true
      VpcId: !Ref CfVPC
      AvailabilityZone: ap-northeast-1a
      Tags:
        - Key: Name
          Value: CfPrivateSubnet
  CfPrivateSubnet:
    Type: AWS::EC2::Subnet
    Properties:
      CidrBlock: 10.1.2.0/24
      MapPublicIpOnLaunch: false
      VpcId: !Ref CfVPC
      AvailabilityZone: ap-northeast-1c
      Tags:
        - Key: Name
          Value: CfPrivateSubnet

  CfInternetGateway:
    Type: AWS::EC2::InternetGateway
    Properties:
      Tags:
        - Key: Name
          Value: CfInternetGateway

  AttachCfInternetGateway:
    Type: AWS::EC2::VPCGatewayAttachment
    Properties:
      InternetGatewayId : !Ref CfInternetGateway
      VpcId: !Ref CfVPC

  CfRouteTableForPublicSubnet:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: !Ref CfVPC
      Tags:
        - Key: Name
          Value: CfRouteTableForPublicSubnet

  CfRouteForPublicSubnet:
    Type: AWS::EC2::Route
    Properties:
      RouteTableId: !Ref CfRouteTableForPublicSubnet
      DestinationCidrBlock: 0.0.0.0/0
      GatewayId: !Ref CfInternetGateway

  CfAssocciateRouteTableForPublicSubnet:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      RouteTableId: !Ref CfRouteTableForPublicSubnet
      SubnetId: !Ref CfPublicSubnet

  NatGatewayEIP:
    Type: AWS::EC2::EIP
    Properties:
      Domain: vpc

  CfNatGateway:
    Type: AWS::EC2::NatGateway
    Properties:
      AllocationId:
        Fn::GetAtt:
          - NatGatewayEIP
          - AllocationId
      SubnetId: !Ref CfPublicSubnet
      Tags:
        - Key: Name
          Value: CfNatGateway

  CfRouteTableForPrivateSubnet:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: !Ref CfVPC
      Tags:
        - Key: Name
          Value: CfRouteTableForPrivateSubnet

  CfRouteForPrivateSubnet:
    Type: AWS::EC2::Route
    Properties:
      RouteTableId: !Ref CfRouteTableForPrivateSubnet
      DestinationCidrBlock: 0.0.0.0/0
      NatGatewayId: !Ref CfNatGateway

  CfAssocciateRouteTableForPrivateSubnet:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      RouteTableId: !Ref CfRouteTableForPrivateSubnet
      SubnetId: !Ref CfPrivateSubnet
      ```
