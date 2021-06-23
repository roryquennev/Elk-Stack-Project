## Kibana Investigation

#### SSH Barrage

Task: Generate a high amount of failed SSH login attempts and verify that Kibana is picking up this activity.

<details>
<summary> Activity File: SSH Barrage </summary>

---

We can easily do this by trying to SSH to a web machine from our jump box directly without using the Ansible container. 

1. Start by logging into your jump-box. 

2.  Run the failed SSH command in a loop to generate failed login log entries.

        - while :; do ssh -T ansible@10.0.0.5; done
    
    ![sshjustoneserver](https://user-images.githubusercontent.com/77551247/123014694-c80f5280-d394-11eb-866c-6ba1a6179fde.PNG)


3. Search through the logs in Kibana to locate your generated failed login attempts.

   ![Log Stream Live - SSH Fail](https://user-images.githubusercontent.com/77551247/123014105-829e5580-d393-11eb-808d-78121c9ec405.PNG)

        
**Bonus**: Create a nested loop that generates SSH login attempts across all three of your VM's:
        
        - while :; do ssh -T ansible@10.0.0.5 | ssh -T ansible@10.0.0.6 | ssh -T ansible@10.0.0.10; done
         
![SSHfailloginloop](https://user-images.githubusercontent.com/77551247/123013886-0dcb1b80-d393-11eb-84e2-e2fe3df17065.png)


          


</details>

#### Linux Stress

Task: Generate a high amount of CPU usage on the pentesting machines and verify that Kibana picks up this data.

<details>

<summary> Activity File: Linux Stress </summary>

---

#### Notes

1. From your jump box, start up your Ansible container and attach to it.

2. SSH from your Ansible container to one of your WebVM's.

3. Run `sudo apt install stress` to install the stress program.

4. Run `sudo stress --cpu 1` and allow `stress` to run for a few minutes. 
![web1stress](https://user-images.githubusercontent.com/77551247/123016094-de6add80-d397-11eb-971b-115104d81860.PNG)

5. View the Metrics page for that VM in Kibana.  What indicates that CPU usage increased?
        
  - Here are our results for Webserver1:
    ![stressnapshotwebserver1](https://user-images.githubusercontent.com/77551247/123018380-723ea880-d39c-11eb-8473-4f3897a8be7f.PNG)
    
    As we can see by running `sudo stress --cpu 1` there is significant stress placed on the overall CPU usage, reaching its maximum. We can also observe a notable spike in the Load for the webserver as well. 


6. Run the `stress` program on all three of your VMs and take screenshots of the data generated on the Metrics page of Kibana.
  - Running the same test on our other web servers, we see the same results replicated regarding the CPU usage and the Load. There remain no discernible increases pertaining to the Memory Usage or Network Traffic
  
  - Here are our results for Webserver2:
    ![stresssnapshotwebserver2](https://user-images.githubusercontent.com/77551247/123019595-cb0f4080-d39e-11eb-86c0-13019ddda7f2.PNG)

  - Here are our results for Webserver3:
    ![stresssnapshotwebserver3](https://user-images.githubusercontent.com/77551247/123019785-28a38d00-d39f-11eb-8fa3-940c188e1827.PNG)

        
</details>


#### wget-DoS


Task: Generate a high amount of web requests to your pen-testing servers and make sure that Kibana is picking them up.

<details>

<summary> Activity File: wget-DoS </summary>

---

The Metrics section for a single VM will show Load and Network Traffic data. 

We can generate abnormal data to view by creating a DoS web attack. The command-line program `wget` can do this easily.

`wget` will download a file from any web server. Use man pages for more info on `wget`.

1. Log into your jump box.

2. Run `wget ip.of.web.vm`.
   ![wgetserver1](https://user-images.githubusercontent.com/77551247/123020038-a798c580-d39f-11eb-8c06-a99126790849.PNG)


3. Run `ls` to view the file you downloaded from your web VM to your jump box. 

   ![jumpboxls](https://user-images.githubusercontent.com/77551247/123020147-d0b95600-d39f-11eb-9a73-187508c138a9.PNG)


4. Run the `wget` command in a loop to generate many web requests.

        - You can use a bash `for` or `while` loop, directly on the command line, just as you did with the SSH command.

5. Open the Metrics page for the web machine you attacked and answer which of the VM metrics were affected the most from this traffic:
        
        - Which of the VM metrics were affected the most from this traffic?
          ![wgetsnapshotwebserver1](https://user-images.githubusercontent.com/77551247/123021029-538ee080-d3a1-11eb-9312-a49eeaa504a2.PNG)


        
**Bonus**: Notice that your `wget` loop creates a lot of duplicate files on your jump box.

-  Write a command to delete _all_ of these files at once.

-  Find a way to run the `wget` command without generating these extra files.
                
        - Look up the flag options for `wget` and find the flag that lets you choose a location to save the file it downloads. 
                
        - Save that file to the Linux directory known as the "void" or the directory that doesn't save anything.

**Bonus**: Write a nested loop that sends your `wget` command to all three of your web VMs over and over.

</details>


---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  

