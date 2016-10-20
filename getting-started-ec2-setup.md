## Unix Shell Session Setup

* [Sign up for an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html)
* Enter your billing address and credit card information. You will not be charged for anything, you just need to put in your payment information. You will only get charged for something if your usage exceeds the free tier limits. For our sessions, we will not exceed this limit (make sure you turn off your VMs when they're not in use to avoid charges)
* If you have Windows, [install PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) so that you can remote login (ssh) to your virtual machine
* If you have a Mac or another linux-based OS, make sure that your security/firewall settings are set so that you can ssh to your virtual machine


## Next Steps
We will do the following steps in our first session, but feel free to go ahead on your own if you would like. There are [comprehensive walkthroughs](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html), help and answers to FAQs in the AWS documentation so you should be able to clarify anything that is unclear here:

* Launch an EC2 instance
	* Use the free-tier, default size instance
	* Choose Ubuntu for your OS
	* Store your ssh key somewhere on your local machine (and remember where you put it!)
	* Change the network/security settings on your instance to allow access from all IP addresses (0.0.0.0)
* SSH into your instance from your terminal
    
    ```
    ssh -i <your ssh key file> ubuntu@<public IP address of instance>
    ```
 
    for example:

    ```
    ssh -i adams-key.pem ubuntu@52.34.56.92
    ```
