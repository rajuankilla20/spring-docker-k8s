# Currecny-conversion-ms-basic & currency-exchange-ms-baisc:

- Auto detection of services discovory with by service name <SERVICE_NAME>_SERVICE_HOST, <SERVICE-NAME>_SERVICE_PORT and we can use these variables 
  - By adding env variable in deployment.yml.spec.spec.containers.image.env: CURRENCY_EXCHANGE_URI , value : http://currency-exchange, as it wont change and no need of dependant on port numbers
- LoadBalancer: Covers the creating of deployment with LoadBalancer for each service 
  - Ingress: Acts as a gatgway for many services instead of having one loadbalancer for each server 
    -  Need to change the LoadBalancer to NodePort and created the ingress file which is work as a gateway
