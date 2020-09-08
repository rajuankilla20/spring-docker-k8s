# Currecny-conversion-ms-basic & currency-exchange-ms-baisc:

- Auto detection of services discovory with by service name <SERVICE_NAME>_SERVICE_HOST, <SERVICE-NAME>_SERVICE_PORT and we can use these variables 
  - By adding env variable in deployment.yml.spec.spec.containers.image.env: CURRENCY_EXCHANGE_URI , value : http://currency-exchange, as it wont change and no need of dependant on port numbers
- LoadBalancer: Covers the creating of deployment with LoadBalancer for each service 
  - Ingress: Acts as a gatgway for many services instead of having one loadbalancer for each server 
    -  Need to change the LoadBalancer to NodePort and created the ingress file which is work as a gateway
# FeignClient - Used to call rest api instead of using RestTemplate 
  - Replacement of RestTemplate to call services and need to add below annotation on ProxyInterface
  -  @FeignClient(name = "currency-exchange", url = "${CURRENCY_EXCHANGE_URI:http://localhost}:8000")
  - @EnableFeignClients("com.rajuankilla20.ms.currencyconversionservice.resource") on Main class
  - Need to add Env variables in deployment.spec.spec.containers.image.env
  - Need to use individual load balancer for each MS.
# Ingress :
   - Ingress: Incoming traffic rules for load balancer 
   - Instead of creating each Load Balancer for each MS , we have Ingress 
   -	We can have multiple path mapping for diff backend based on path and etc mapping., with ports mention 
   -	It will assume by default service-name as path 
   -	Once ingress in created change the Load Balance to Node Point as we are not exposing directly to client
# RibbonClient - use for client side load balancing  
  - Workes as client side load balancer and to discover k8s services using api we have to apply 
  - no need of any env variables for services names
  - we have to do @EnableDiscoveryClient along with @EnableFeignClient ( which we use for calling proxy services)
  - we have to provide ServiceAccount access to the k8s cluster using CusterRoleBinding rbac.yml file
# spring-cloud-started-kubernetes using 
# Docker images for these two services 
    - rajuankilla20/currency-conversion:0.0.1-RELEASE
    - rajuankilla20/currency-exvhange:0.0.1-RELEASE

