# Create a custom Helm chart

1. To create a helm chart template 
   ```sh 
   go to /home/ubuntu
   helm create ttrend
   ```

    by default, it contains 
    - values.yaml
    - templates
    - Charts.yaml
    - charts

2. Replace the template directory with the manifest files and package it
   ```sh
   cd templates
   rm -rf *
   # move all manifest files under templates directory
   helm list
   kubectl get all -n valaxy   # delete if any resources is created
   helm package ttrend
   ```
3. Change the version number in the 
   ```
   helm install ttrend ttrend-0.1.0.tgz
   helm list
   ```

4. Create a jenkins job for the deployment, add zip file into source code, so that will also be cloned.
   ```sh 
   stage(" Deploy ") {
          steps {
            script {
               echo '<--------------- Helm Deploy Started --------------->'
               sh 'helm install ttrend ttrend-0.1.0.tgz'
               echo '<--------------- Helm deploy Ends --------------->'
            }
          }
        }
   ```

5. To list installed helm deployments
   ```sh 
   helm list -a
   ```

Other useful commands
1. to change the default namespace to valaxy
   ```sh
   kubectl config set-context --current --namespace=valaxy
   ```
