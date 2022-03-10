**ConfigMap:**

Generally we use ConfigMap when we want to pass parameters to an Image. Some applications/images need parameters to run them on different environments like testing, staging, UAT, production etc, during that time it is not a good idea to add this parameters directly into an Image file because in that case it will be difficult to manage it when we want to push those images/PODs on to different environments. 

Every environment have different parameters, settings, API’s. Hence, it’s a good idea to maintain these settings/parameters on a different file or configuration so that we can attach these configurations to the image/PODs depending on the environment it is being used.

We can create a ConfigMap using Imperative method or Declarative method.

**There are two ways by which we can create a configMap** 

**Imperative method One:** 

First we are adding all the settings/parameters into a file called config.txt as shown below

![image](https://user-images.githubusercontent.com/26220908/157751320-f882a6d6-18d1-4d34-9a77-d45bca84305e.png)

Now, we used the above file to create a configMap as my-config as shown below.

![image](https://user-images.githubusercontent.com/26220908/157751878-e0728de1-bdad-4941-813e-7942fe2197db.png)

You can see the configuration below:

![image](https://user-images.githubusercontent.com/26220908/157751960-a35c2cf7-6af1-4833-b83e-b1a6a2fddf16.png)

**Imperative method two:**

You can use –from-literal to create parameter and their values as shown below

![image](https://user-images.githubusercontent.com/26220908/157752039-70b1ccdf-bea9-45a4-943c-cf7996f9a5c3.png)

You can see how the configurations are created

![image](https://user-images.githubusercontent.com/26220908/157752122-0e4b3fe9-22bd-440e-82e9-b148af7866ca.png)

\=================================================================================

Now, we have to attach these ConfigMaps to PODs. Let’s see how we can do this.

We can attach ConfigMaps to PODs in 3 ways.

![image](https://user-images.githubusercontent.com/26220908/157752214-e3ef050f-1b2d-44dd-9b2c-acf3c3473932.png)

Let’s first create a YAML file to create a 3 PODs to show the example

![image](https://user-images.githubusercontent.com/26220908/157752267-ef9c971b-4c7a-46ad-8bfd-27a1be66e3d5.png)

Now, we created 3 PODs, let’s begin with the First method:

**1st Method -** 

Here, we are editing the *app1.yaml* file for attaching the **ConfigMap** details which we created ( *firstName*, *lastname* and *country* which are part of *my-config* **ConfigMap**)

![image](https://user-images.githubusercontent.com/26220908/157752355-45bb0b88-e1f8-4979-bb3b-3d600a3716c5.png)

After attaching the **ConfigMap** details to the **POD** app1, we can create the POD **app1** which will be attached with **ConfigMap** details of *my-config* which we created earlier.

![image](https://user-images.githubusercontent.com/26220908/157752431-c5cb1502-0eab-47d9-a922-29ba87f1308f.png)

The POD app1 is in running state as we can see above. Now, let’s get into the POD app1 to see if the ConfigMap details are attached to the POD or not.

![image](https://user-images.githubusercontent.com/26220908/157752483-4d60e96b-e08b-4f15-9e52-5c6bd89f4c60.png)

After seeing the above screen, it is confirmed that the configuration of my-config is attached to the POD app1 (Highlighted in Yellow).

\=====================================================================================

**2nd Method – How to pass custom variables of ConfigMap to a POD**

Now, let’s update the app2.yaml file to attach the ConfigMap changes.

![image](https://user-images.githubusercontent.com/26220908/157752549-7a34374d-392e-499a-8580-85d4fa780369.png)

Here, we are just adding the ConfigMap (my-config) to the POD (app2) as highlighted below. So that it can take all the configurations which are part of my-config to the POD app2.

![image](https://user-images.githubusercontent.com/26220908/157752589-f2987171-7884-4cc5-b035-b11d493e72be.png)

After updating the changes, we can see that the POD app2 is in Running state.

![image](https://user-images.githubusercontent.com/26220908/157752661-6e54303d-0d47-4106-98a4-21ae7237799d.png)

Lets get into POD app2 in a interactive mode and check our configuration changes are updated to POD or not.

![image](https://user-images.githubusercontent.com/26220908/157752712-efa3be02-ce93-4f86-b11a-6424110e478a.png)

After seeing the above screen, we can confirm that the ConfigMap (my-config) changes are applied to the POD (app2) which are highlighted.

3rd Method – In this method we will mount the ConfigMap my-config configurations to the POD using the volumeMount. Here, we are adding the configurations of my-config to the POD at the path “/etc/config-details” as highlighted below.

![image](https://user-images.githubusercontent.com/26220908/157752761-b5da3cd4-43d7-463c-a998-7d8f3802759d.png)

Lets apply the changes which we made to the POD app3

![image](https://user-images.githubusercontent.com/26220908/157752802-d20150a1-c845-44e2-892e-37aeb25a6e9e.png)

After applying the changes we can see that the POD app3 is in Running state

![image](https://user-images.githubusercontent.com/26220908/157752876-d68107f9-a472-458c-ae30-b3f2739c8c2b.png)

Now, let’s confirm if the changes of my-config is attached with the POD app3 or not.

![image](https://user-images.githubusercontent.com/26220908/157752913-fc2c31e4-32f0-43c5-8125-d0ccc74e74ef.png)

After seeing the above screen, it is confirmed that the POD app3 is updated with the ConfigMap configuration of my-config.

**NOTE: Here, in this document I demonstrated**

1. **How to create ConfigMap.**
1. **How to create PODs.**
1. **How to attach ConfigMap to a POD (Shown 3 different methods for this)**
