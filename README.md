# Resource hierarchy
 Each GCP resource (compute engine, Stackdriver monitoring, Cloud SQL, etc) is attached to a single GCP project which may or may not be arranged within folders representing the departments in an organisation:  
 
<div align="center">
 <p>organisation(/Individual user)</p>
 <img src="https://render.githubusercontent.com/render/math?math=\uparrow">
 <p>folder</p>
 <img src="https://render.githubusercontent.com/render/math?math=\uparrow"> 
 <p>project</p>
 <img src="https://render.githubusercontent.com/render/math?math=\uparrow">
 <p>resource</p>
</div>
 
   **example**: 
<div align="center">
 <p>Google</p>
 <img src="https://render.githubusercontent.com/render/math?math=\uparrow">
 <p>Workspace</p>
 <img src="https://render.githubusercontent.com/render/math?math=\uparrow"> 
 <p>GMail</p>
 <img src="https://render.githubusercontent.com/render/math?math=\uparrow">
 <p>Compute engine</p>
</div>

# Identify and Access Management   
 Control access to resource following the principal of least privilages while assigning resources to roles.  
 
<div align="center">
 <p>resource <img src="https://render.githubusercontent.com/render/math?math=\leftrightarrow"> access_type <img src="https://render.githubusercontent.com/render/math?math=\leftrightarrow"> user/identity</p>
</div>

# Stackdriver workspace (Cloud monitoring/Debugging)  
 **Logging**: allows to store search and set alerts for log data within GCP,  
 **Monitoring**: provides visibility into the performance, uptime and overall health of cloud applications, by collecting metrics events and metadata from GCP.   

# Compute options  
  
  Compute enginer:   
   * For creating monolithic applications   
   * Already managing VMs in on-premise environment or other cloud platform, and to obtain similar performance.  
  
  Kubernetes engine:   
   * if application is containerized, and  
   * micro-service based   
  
  App-engine:  
   * Lets user concentrate only on the application development and code, without having to configure any aspect of the infrastructure.  
   * Appengine-flexible:   
      * runs on containers  
       * More feature support for AB testing, rerouting and so on.  
  
  Cloud functions:  
   * To write simple single purpose functions attached to events empted from cloud services.  
   * Event driven  
   * Can only write code/funcion in certain set of languages  
   * Short-run application  
  
  Cloud run:  
    * Managed service for stateless containers.  
    * Minimum management
    
## Google compute engine 
  * Is used for provisioning and managing cloud VM instances.  
  * **Load balancing** and **autoscaling** can be implemented when provisioning multiple VM instances  
      *(autoscaling:- Alter the number of actively running instances based on the load on application resources.)*
  * Can attach storage to VMs 
  * Network connectivity and configuration can be done to allow access on specific ports, expose instance to a specific IP address (reserved or ephemeral)
  * Machine families available:   
      * general-purpose - Best price/performance ratio  
      * compute-optimized - For scientific research, gaming applications   
      * memory-optimized - When lot of ram required  
      * GPU  
  * Public image and custom images can be installed in VMs
  * For a specific VM External IP (which is unique for all resources) is internet accessible, whereas internal IP (Two separate corporate resources can have same internal IP address) is only accessibly within a subnet/VPC in the google cloud network.  
  * Static (reserved) external IP addresses can be switched from one VM instance to another within the same project, and they remain attached to the VM even when the VM has been stopped. A particular billing characteristic to be noted on static IP addresses is that the **user/organisation is billed for the static IP when it is not in use**
  * Startup script allows to install latest image package updates and install and run webserver templates during VM instance creation. But this increases boot-up time.  
  * Instance template can be used to speed-up the VM creation process by having all properties pre-configured. The same can also be used to created managed instance groups. Instance templates are immutable.  
  * Custom images (With OS patches and softwares pre-installed) can be created from an instance, persistant disk, snapshot, another image, or file in cloud storage. That can be shared accross projects. An image can be **hardened** with specific corporate security standards and distributed for efficient and smooth workspace setup. Custom images are preferred over startup scripts since they do not have bootup overhead. Although custom images facilitate installation of OS patches and softwares, creation and manipulation of files and/or services need to be done using startup scripts while creating an instance or an instance template using the custom image.   
  * **Live migration**: To keep VM instances running when a host system needs to be updated the VM instances are migrated to another host within the same zone (Not supported by GPUs and preemptible VMs). and this can be configured using **Availability policies**. The two available important policies include *On host maintainance* (default: migrate, other options: terminate, and *automatic restart* to automatically restart VM instances that terminated due to non-user-initiated reasons (maintenance event, hardware failure, etc).  

### Unmanaged instance groups 
  They are used when we would like to do most of the management ourselves, though they aren't really recommended and are designed for heterogenous clusters,  
  eg: migrating a particular cluster that is on premise and you'd like it to run exactly as it is on google cloud.  
  
### pre-emptible machines   
  They cost 70% less than regularly charged VM, no control over the shut down of VM - can be shut down by GCP at any time (preempted) within 24hrs (with 30s warning).
  Cannot alter number of available VMs.  
  
  Used for:  
   * Fault tolerant application  
   * cost sensitive scenario  
   * When workload is not immediate such as non-immediate batch-processing jobs  
  
  Restrictions:    
   * Not always available   
   * No SLAs   
   * Can't be converted to regular VMs   
   * No automatic restarts   
   * Free tier credits are not applicable to launch these.   

### Cloud run 
  It runs containers not VMs, supports autoscaling but requires restructuring application as docker image to implement it.  
  It is a managed service for running containers, and they must be stateless (can't have persistant disk attached).  

## App engine  
 * Standard:  
    Language specific sandbox based service   
 * Flexible:  
    Can specify custom docker image to run in appengine.  

## Kubernetes engine
  Commands that start with `gloud cluster` are used to manipulate the cluster themselves, whereas `kubectl` commands are used to manipulate things inside the cluster such as the node-pools, pods etc.   

## Anthos
  Hybrid cloud service used to manage Kubernetes clusters in any cloud platform from one location, easy and efficient management of workload.


# Cloud pub/sub 
  Allows to decouple services, say frontend and backend in instances where you need to scale your application the frontend scales far more efficiently (owing to their stateless nature) compared to the backend (cloud SQL database service), therefore it becomes necessary to make the frontend instead communicate to a cloud pub/sub topic where tasks can be queued up and allowing the backend services to consume these tasks at whatever rate that it can without lose of data.  
  
  Important from a scalability perspective.  
  
  Note: The maximum permissible size of data is 10MB, larger data that needs ETL processing of larger data cloud storage can be used where data is stored in a bucket. Cloud pub/sub can be used in this case to send url that points to bucket and file for the next service/process to use.  

# Managed services 
## Cloud Dataproc
  * Managed hadoop and spark service  
  * Big data processing  
  * To migrate from onpremise hadoop cluster  
  * Preparing data, data processing pipelines.

## Dataflow
  * Data processing pipelines  
  * Stream-processing and batch-processing of data  

## Dataprep
  * Preparing data for machine learning

## Datalab
  * Interactive tool for exploring data 

# Networking   
  4 categories of networking components available:  
   * Connect:   
     * **Cloud VPN** and **Cloud Interconnect** help connect on-premise resources to GCP and establish a secure channel between them.    
     * **Cloud VPC**: Virtualized network subnets   
   * Scale:   
     * **Cloud Load balancing** scaling of backend instances based on incoming  traffic  
     * **Cloud CDN** allows caching objects closest to the user accessing it to reduce latency.  
   * Optimize:  
     * **Standard Network Tier**(Optimize for cost) and **Premium Network Tier**(Optimize for performance) variants available.  
   * Secure:  
     * **Identity Aware Proxy** and **Cloud Armour** allows to secure applications on the internet to prevent unauthorized (malicious) activities.   

## Cloud armour
  * Web-application firewall at layer 7(OSI model), rules are associated with application logic layer, to control the incoming data - http traffic and so on.  
  * Protect webapplication against DDOS attacks  
  * Allows us to specify our own package check logic on incoming requests/data 

# Storage  
## Big Query:  
  uses columnar storage  

## Datastore/firestore:  
  * document based  
  * json formatted  
  * Flexible schema  
  
## Bigtable:  
  * organizing principle -> sparse multidimensional map  
  * Cluster of VMs that manage metadata about the data. The data is stored in the colossus filesystem. The way the keys are structured determines which block the data is going to be written to. If all the keys are sequential then we get a hotspot were data is written to the same block.  

## Cloud Storage
  * Allows setting policies to cloud storage buckets, to automatically delete/create files, to move file to nearline/coldline storage after certain period of time.
  * Migrating from on-premise legacy hadoop cluster using HDFS (hadoop filesystem), to use this in gcloud we can map HDFS to (through dataproc) cloud storage.  
  * Multi-region cloud storage buckets replicate the data redundantly across several regions for it to be accessible to users with low latency and high availability.   
  * 

# Billing 
 * Pricing calculator available to plan and estimate GCP products usage.  
 * Users/Organisations are billed by the second after a minimum period of 1 minute.   
 * And stopped VM instances are not billed unless it has attached storage.  
 * Budget alerts can be created to be notified on the charges based on resource utilization.   
 
## Sustained usage discounts
  * Sustained usage billing discounts for more than 25% usage in a month vary from 20%-50%, and the discount increases with usage.   
  * Applicable to both google compute engine and kubernetes engine.  
  * Does not apply to A2 and E2 machine types as well as instances created using app-engine flexible and dataflow resources.  
  * **Commited usage discounts** require user/organisation commitment based on predictable resource requirements from a certain period of time (1-3 years), and the discount upto 70% can be obtained based on machine type and GPU. Same restrictions as those for sustained usage discount apply.    
 
  
  
