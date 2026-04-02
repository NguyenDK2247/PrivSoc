# **Week 3: Open-source Intelligence** 

What information is publicly available about you?
The amount can surprise you.

In the exercises this week we go through some popular methods and sources of openly available information.

> We highly recommend the task 3!

## Grading

You must do tasks **in order**.

You are expected to use more time on later tasks to get an equal amount of points than in previous tasks.

The bonus task is not counted toward the course's maximum possible points; it is extra and can compensate for other work.

Task #|Points|Description|
-----|:---:|-----------|
[Task 1](#task-1-have-i-been-pwned) | 1 | Have I been Pwned 
[Task 2](#task-2-hardcoded-passwords) | 1 | Hardcoded passwords
[Task 3](#task-3-osint-exploitation) | 2 | OSINT exploitation
[Task 4](#task-4-blockchain-bonus) | 1 | Blockchain (bonus)


## **Task 1:** Have I been Pwned

One of the most typical and critical situations for a person could be the case when their login credentials have been leaked online publicly as a part of a cyber incident or another matter.

[Have I been Pwned](https://haveibeenpwned.com/) is a site that tracks occurrences of emails and phone numbers in various data leaks.

### **Task 1 A)** Looking for leaks

Search for ***joe@gmail.com*** on Have I been Pwned, and...  

<details>
<summary><strong>Answer the following:</strong></summary>
<br>

In how many <strong>data breaches</strong> and <strong>pastes</strong> can this email be found?

**Answer:** The ***joe@gmail.com*** email has a total of `320` data breaches and `96` pastes.

What are the <strong>compromised data types</strong> in the following services? (answer each separately)

- <strong>Bell</strong>
    - **Answer:** `email address`, `geographic locations`, `IP addresses`, `job titles`, `names`, `passwords`, `phone numbers`, `spoken languages`, `survery results`, `usernames`.
- <strong>Drizly</strong>
    - **Answer:** `dates of birth`, `device information`, `email addresses`, `IP addresses`, `names`, `passwords`, `phone numbers`, `physical addresses`.
- <strong>Robinhood</strong>
    - **Answer:** `email addresses`.

</details>

> While you are at it you might want to check if **your own email addresses** have been associated with any data leaks, and promptly change your password in these services.

> Remember that when entering your email, password or phone number, you ultimately trust the service provider not to misuse this information.

### **Task 1 B)** Breach data content

However, "have I been pwned" service tries to limit what data it shows to you.
Owning and sharing too private information can lead to legal troubles and controversial opinions.

Some sensitive services might on their own tell too much about the owner of the email address, as anyone can look for anyone's email addresses, phone numbers and passwords.
As a result, for example, sometimes you need to verify the email address before you can see all breaches the address has been part of.

On the other hand, some other services distribute all breach data content, as paid services.
As the information is highly valuable for some entities, these entities will pay for the data, and platform providers will run the services until law enforcement will shut them down.

1. **Find at least three of these paid services and list them.**

    **Answer:**
    - [Breachsense](https://www.breachsense.com)
    - [DarkOwl](https://www.darkowl.com)
    - [DeHashed](https://dehashed.com)

*Consider the problems of breach data as follows*. 

Would it be better to build platforms which make **all** breach data searchable for everyone, or identified persons? Or instead, try to remove it from the internet? Which might be impossible.

Eventually, if the breach happens, the information is obtainable with or without money in the end.

Would it be better for the end user to see what has been leaked precisely?
Or would it be better that **maybe** the data has been removed from the internet, and there is no verification of what this data is?

In many cases, the breached company cannot always say what data has been lost, or they are unwilling to do it, or downplays the impact.

Could it change the way we think about privacy, and how we use services and prioritise security if the breach data is public?

Or do we make a compromise, and try to remove only the most damaging breaches from the internet?

2. **Write a short answer (150-200 words) of your thoughts. There might not be a correct or incorrect answer, but you need to make arguments.**

    **Answer:** There is no easy answer to the question of what to do with breach data. There are pros and cons with each choice, and all of them can bring about dire consequences to consumers/companies.

    One option is to make breach data public for everyone to see. This way, people know exactly what was leaked about them, therefore raising awareness about their security weaknesses and important credentials to avoid giving, should this happen again. On a broader scale, it can also pressure companies to improve their security measures against such attacks. However, this comes with a heavy price: hackers and attackers now have information easily and can use it for identity theft to mask their attacks even further.

    If publicizing breach data is not so good an option, one can debate removing such information from the Internet, for good. Data might be harder to find, because you are attempting to erase it from the Internet archives and any source related to it, but data also spreads like wildfire and once the data breach has been initiated, it keeps multiplying itself through devices, hardware, software, etc. and therefore becomes nearly impossible to stop it. It can create a false sense of security as well, since removing data from the Internet simply is not deleting them and pretending they are gone. Somewhere, some way, there will always exist a way to recover those files and you might not even know that it's already underway.

---

## **Task 2:** Hardcoded Passwords

There have been a few cases of compromised systems due to hardcoded passwords and API keys accidentally ending up in production code. [Google offers some advice on how to handle such information more securely](https://cloud.google.com/docs/authentication/api-keys)

1.  Use Hex-Rays decompiler via [Dogbolt](https://dogbolt.org/) to check out if you can find a **plaintext hardcoded password** from the provided compiled C code file called **secretKey**. 

2. As a second part, there is a secret **Activation Key** for you to figure out, which has validation arguments that can be seen with some closer inspection of the decompiler.

3. As a third and last part, there is a **Super secret password** that is hardcoded but has been "encrypted" with a secret hash.


In case the site is under maintenance, there is a HexRaysOutput file, which has the full output of the decompilation process.
Use an editor that can understand `C++` to inspect the file with proper highlighting.

You can run the C program to validate your findings in your terminal by navigating to the same folder where the file resides and using the command **./secretKey** on `glibc` Linux system.

After completing the task, you have five items to return. 

<details>
<summary><strong>What to return:</strong></summary>
<br>

Return a valid <strong>Password</strong> and  
<strong>One valid activation key</strong> and  
The <strong>instructions</strong> on how to create the rest of the activation keys, since there are multiple valid ones.  
Also, return the <strong>plaintext version of the super secret password</strong> and <strong>the name of the hash function</strong> it was created with.   
You can use for example https://crackstation.net/ to decode the password.

**Answer:**
- **Password** can be found in the `strcpy(s2, "Vulture35Vulture");` line. The password is `Vulture35Vulture`.
- **Activation key** can be found following the logic shown in this block of code:
``` c
v7 = strtol(nptr, &endptr, 10);
v6 = sum(v7);
if ( v7 > 59347700 && v7 <= 59347970 && v6 == 44 )
    break;
```

- According to the code, the activation key `v7` needs to follow these two **instructions**: 
    - Be between `59347700` and `59347970`
    - Has `44` as the sum of its digits. 

- **One such key** that satisfies the conditions is `59347790`.
- The hashed version of the super secret password is `4dc9332ca3bbc59c880fd2cbe7ec1b7ca171cc82`. Pasting this in [crackstation.net](https://crackstation.net) yields us its **plaintext version** is `Vulture99` using **type** `sha1`.

</details>

---


## **Task 3:** OSINT exploitation

> **Note**
> ~~To do this task, you need to be connected to the University of Oulu VPN or have to be connected to the EDUROAM network on campus:~~
~~Instructions for connecting:~~
~~https://ict.oulu.fi/16863/~~


You have applied for a job at Pelle Security, the new clown-themed cybersecurity startup.
As a last-round interview assignment, you are tasked with performing OSINT on the company.

Start the task by finding possible social media accounts used for marketing by the company.

Your end goal is to infiltrate the company's server. The server is located at 172.232.132.8

Feel free to use tools such as:

Installation instructions are for the course arch virtual machine.

- [Sherlock](https://github.com/sherlock-project/sherlock)

    ``` sudo pacman -Sy sherlock```
- [Breachdirectory](https://breachdirectory.org/)
- [ReconFTW](https://github.com/six2dez/reconftw#osint)

    ```
    git clone https://github.com/six2dez/reconftw.git 
    cd reconftw/
    ./install.sh
    ```
- [Hashcat](https://hashcat.net/hashcat/)

    ```sudo pacman -Sy hashcat```
- [John the ripper](https://github.com/openwall/john)

    ```sudo pacman -Sy john```
- [Spiderfoot](https://github.com/smicallef/spiderfoot)

    ```
    wget https://github.com/smicallef/spiderfoot/archive/v4.0.tar.gz
    tar zxvf v4.0.tar.gz
    cd spiderfoot-4.0
    pip3 install -r requirements.txt
    python3 ./sf.py -l 127.0.0.1:5001
    
Note that not all of these are needed.

## Answer this task with screenshots for all parts listed below

### 1. What is the alias of the new employee and where is he from? Explain where you found this information

**Answer:** Pelle Security has a GitHub account, and it can be found on [`https://github.com/PelleSecurity`](https://github.com/PelleSecurity). The alias of the new employee is `SecurityPelle` and the location is `Oulu`.

![alias & location](/3.Open-source_intelligence/screenshots/1.%20alias%20&%20location.png)

### 2. What is the employee's real name? Explain how you found it.

**Answer:** The employee's real name can be found in the `77711c4` commit in the `PelleWeb` repository when looking at past commits. His name is `Klovni`.

![real name](/3.Open-source_intelligence/screenshots/2.%20real%20name.png)

### 3. The employee may have accidentally leaked his email address. Find the password of this leaked email. Explain where you found it:

### 4. Explain how you logged into the SFTP server. What was the password?

<details>
<summary><strong>Hint:</strong></summary>
<br>
People often use only a part of their name to login to their computers.
</details>

### 5. What is in the flag.txt file located on the SFTP server?

### 6. Now finish the task by logging into the company's server. Explain how you did this.

### 7. What is in the text file located on the server?

---

## **Task 4:** Blockchain (bonus)

We will take a brief look at online tools available for inspecting the Bitcoin blockchain.

Just as a quick recap: **Blockchain** is a distributed ledger containing the information as blocks, which are securely linked together with cryptographic hashes.
Well-known examples of blockchains are cryprocurrency ledgers that contain all the transactions made with said cryptocurrencies. 

Incoming transactions are added as **blocks** into the blockchain when a valid **hash** is found for a certain block.
These hashes are brute forced aka **mined** mainly using the processing power of Graphics Processing Units (GPU).

Early Bitcoin developer Laszlo Hanyecz was allegedly one of the first to invent GPU mining.
However, what he is remembered for is the first documented purchase of goods using Bitcoin, where he traded **10,000** Bitcoin for **2 Pizzas**.

You can find conflicting information on the internet about the pizza parlour where the pizzas were bought from.
Aside from that, by inspecting the blockchain we can find the exact information about the transaction.

> Use the [Blockchain explorer](https://www.blockchain.com/explorer) to inspect block **57043** and...  

<details>
<summary><strong>Provide the following information:</strong></summary>
<br>


Transaction
- Date and Time of the transaction
- Hash of the transaction
- Address of sender
- Address of receiver
- Transaction fee amount in bitcoin

Receiver Address
- Who was the owner of this address? Use Google to figure out the real name of the user
- The owner instantly divided and forwarded the 10,000 to (**how many?**) other addresses
- Addresses that received the 10,000 bitcoin and the corresponding sums to each address

Block
- Hash of the block 57043
- Amount of transactions in the block
- Block reward amount

Miner
- Address of the miner for block 57043
- Has this address spent the block reward they received?

</details>


>**[Maltego](https://docs.maltego.com/support/solutions/articles/15000008703-client-requirements)** is a great tool for blockchain tracing.
It lets you create a tree-like structure out of inbound and outbound transactions from different addresses. We recommend checking it out.  
It requires registration.
