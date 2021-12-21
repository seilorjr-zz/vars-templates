## vars-templates

azure devops yaml pipelines (templates)

Example of one deployment template for many enviroments

Example of usage

resources:
  repositories:

  - repository: template      
    type: github
    endpoint: seilorjr
    name: seilorjr/vars-templates
    
  - repository: current      
    type: github
    endpoint: xxxx
    name: youcurrentrepository

    

trigger:
- main

pool:
  vmImage: ubuntu-latest

stages:
  - template: build-app.yml@template
  - template: function.yml@template
    parameters:
      environment: dev  
  - template: deploy-app.yml@template
    parameters:
      environment: dev
      DependsOn: build
  - template: function.yml@template
    parameters:
      environment: qa
  - template: deploy-app.yml@template
    parameters:
      environment: qa
      DependsOn: 
      - deploy_dev
      - build   


