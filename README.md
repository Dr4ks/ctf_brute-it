# ctf_brute-it

Hello everyone, today we will solve ctf named "Brute It" on tryhackme platform. <br />
You can also access to this CTF and try to solve and share opinions with me. <br />

Room Link=> https://tryhackme.com/room/bruteit <br />

Key Words for CTF=> Brute-force,hash cracking, privilege escalation <br />

<br />
Our Ip=> 10.18.8.247
Machine Ip=> 10.10.43.213
<br />

Nmap Scan=>Here, first of all ,we need to recon that's why just using nmap. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/nmap_scan.png)

Just using nmap scan, we just solve first 4 tasks of Task 2 <br />

Directory Enumeration=>It's time to enumerate endpoints of website. From here we just 'admin' endpoint <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/dir_enum.png)

Source Code review=>From here, we just see in comments that , to login from admin panel username=admin shown. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/source_code.png)

Brute Force=>Here, we need to use hydra tool to brute force pass of admin username. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/hydra_payload.png)

Result of brute-forcing is great for us just because we found password 'xavier' and can access to admin panel. <br />
username=admin&pass=xavier <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/result_hydra.png)

We just solve the two tasks of Task 3 by accessing to admin panel <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/admin_panel.png)

Now it's time to use john to crack RSA private key which is located admin panel. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/rsa_key.png)

First of all we need to convert this into hast by using ssh2john tool then starting to crack. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/cracked_pass.png)

Now it's time to get shell, first of all we need to chmod of id_rsa to 600 and then use it to login. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/connec_using_rsa.png)

As we get connected, can see user.txt file. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/user_txt.png)

Until here, we finished 75% of CTF, now time to privesc <br />

For these, we just check sudo -l command to see actions for privilege escalation. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/privesc_enum.png)

Let's find appropiate payload for '/bin/cat' in gtfobins. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/file_read.png)

We know the way , let's read /etc/shadow file to find root's hashed password. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/root_hashedpass.png)

Finally, time to crack password of root.For this we use hashcat tool. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/hashcat_payload.png)

Get result of cracking, and know that password of root user is 'football' <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/hashcat_result.png)

CTF is already finished after reading root.txt file. <br />
![image](https://github.com/Dr4ks/ctf_brute-it/blob/main/images/root_txt.png)


