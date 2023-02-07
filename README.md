# vaultwarden

To test the vaultwarden helm chart, clone the repository, cd into the vaultwarden directory, and run the following commands:
1) helm dependency update
2) helm install [name} ./vaultwarden

This is an example of a Helm chart that is utilizing a common Helm Library Chart to provide boilerplate templates to reduce the complexity in creating Helm Charts.

The following common libary chart was utilized.
https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common to configure the vaultwarden application.

You can design your own new Helm Chart that leverages the common library chart via the following process:

0) Clone this repository
1) Create a new heml chart:  "helm create [new-chart-name]"
2) Removes unnecessary files:
    - rm -rf [new-chart-name]/templates/*
    - rm -rf [new-chart-name]/values.yaml
3) Copy starter files into helm chart directory:
    - cp ./starter-files/values.yaml  ../[new-chart-name]/values.yaml
    - cp ../starter-files/common.yaml ../[new-chart-name]/templates/
    - cp ../starter-files/NOTES.txt ../[new-chart-name]/templates/
4) Configure Chart.yaml
    - edit /../[new-chart-name]/Chart.yaml using ../starter-files/Chart.yaml.example as a reference
    - run "helm dependency update"
  
9) Validate chart is ready for application configuration:
   - Check to see if manifests render -- run: "helm template <name> ."
     
   - Execute a test deployment -- run: "helm install [instance-name] ."
     note: An nginx pod will deploy; this validates that the common library chart is properly wired and you are ready to design your application.  Follow the          helm notes to validate deployment.
  
10) Design your application: 
    Leverage the properties in the values.yaml file to configure your application. The values.yaml exposes all configurable properties from the common library       chart; if you do not edit a property then the default value will be used that is located in the values.yaml file. 
    - To get started: Alter the image properties with your application image and specifications.
        image:
        repository: nginx 
        tag: latest 
        pullPolicy: IfNotPresent

 
Things to know:
  - The common library chart must be added to the Chart.yaml file (see Chart.yaml.example)
  - When execute the command: "helm dependency update"; all dependencies will be downloaded in the ../[new-chart-name]/charts directory as tar files; DO NOT UNTAR THEM.                                                          
  - The common.yaml and NOTES.txt files must be placed in the ../[new-chart-name]/templates directory; the common.yaml file specifies to utilize the common library chart.
 
