We want an automated way to try the common passwords or the entries from a word list; here comes THC Hydra. Hydra supports many protocols, including FTP, POP3, IMAP, SMTP, SSH, and all methods related to HTTP. The general command-line syntax is: hydra -l username -P wordlist.txt server service where we specify the following options:

-l username: -l should precede the username, i.e. the login name of the target.
-P wordlist.txt: -P precedes the wordlist.txt file, which is a text file containing the list of passwords you want to try with the provided username.
server is the hostname or IP address of the target server.
service indicates the service which you are trying to launch the dictionary attack.
Consider the following concrete examples:

hydra -l mark -P /usr/share/wordlists/rockyou.txt 10.10.47.112 ftp will use mark as the username as it iterates over the provided passwords against the FTP server.
hydra -l mark -P /usr/share/wordlists/rockyou.txt ftp://10.10.47.112 is identical to the previous example. 10.10.47.112 ftp is the same as ftp://10.10.47.112.
hydra -l frank -P /usr/share/wordlists/rockyou.txt 10.10.47.112 ssh will use frank as the user name as it tries to login via SSH using the different passwords.
There are some extra optional arguments that you can add:

-s PORT to specify a non-default port for the service in question.
-V or -vV, for verbose, makes Hydra show the username and password combinations that are being tried. This verbosity is very convenient to see the progress, especially if you are still not confident of your command-line syntax.
-t n where n is the number of parallel connections to the target. -t 16 will create 16 threads used to connect to the target.
-d, for debugging, to get more detailed information about what’s going on. The debugging output can save you much frustration; for instance, if Hydra tries to connect to a closed port and timing out, -d will reveal this right away.
Once the password is found, you can issue CTRL-C to end the process. In TryHackMe tasks, we expect any attack to finish within less than five minutes; however, the attack would usually take longer in real-life scenarios. Options for verbosity or debugging can be pretty helpful if you want Hydra to update you about its progress.

In summary, attacks against login systems can be carried out efficiently using a tool, such as THC Hydra combined with a suitable word list. Mitigation against such attacks can be sophisticated and depends on the target system. A few of the approaches include:

Password Policy: Enforces minimum complexity constraints on the passwords set by the user.
Account Lockout: Locks the account after a certain number of failed attempts.
Throttling Authentication Attempts: Delays the response to a login attempt. A couple of seconds of delay is tolerable for someone who knows the password, but they can severely hinder automated tools.
Using CAPTCHA: Requires solving a question difficult for machines. It works well if the login page is via a graphical user interface (GUI). (Note that CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.)
Requiring the use of a public certificate for authentication. This approach works well with SSH, for instance.
Two-Factor Authentication: Ask the user to provide a code available via other means, such as email, smartphone app or SMS.
There are many other approaches that are more sophisticated or might require some established knowledge about the user, such as IP-based geolocation.
Using a combination of the above approaches is an excellent approach to protect against password attacks.