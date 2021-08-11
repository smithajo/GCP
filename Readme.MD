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
 

## Unmanaged instance groups 
  They are used when we would like to do most of the management ourselves, though they aren't really recommended and are designed for heterogenous clusters,  
  eg: migrating a particular cluster that is on premise and you'd like it to run exactly as it is on google cloud.  
  
## pre-emptible machines 
  They cost 70% less than regularly charged VM, no control over the shut down of VM, doesn't alter number of available VMs  

## Cloud run 
  It runs containers not VMs, supports autoscaling but requires restructuring application as docker image to implement it.  
  
  
