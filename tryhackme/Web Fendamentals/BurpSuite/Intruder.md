## Attack types
### 1. Sniper

**The "One-at-a-Time" approach.**

Sniper uses a **single payload set** (one list). It goes to the first position, tries every item in the list, then moves to the second position and tries every item there.

- **How it works:** If you have 10 usernames and 10 passwords, it will try the 10 usernames (keeping the password static), then try the 10 passwords (keeping the username static).
    
- **Total Requests:** $n \times p$ (where $n$ is the number of payloads and $p$ is the number of positions).
    
- **Best For:** Fuzzing individual parameters for common vulnerabilities like XSS or SQL injection.
    

### 2. Battering Ram

**The "Mirror" approach.**

Like Sniper, it uses a **single payload set**, but it puts the **same value** into every position simultaneously.

- **How it works:** If your payload is `admin`, it sends `username=admin&password=admin`. It then moves to the next word in the list and repeats.
    
- **Total Requests:** $n$ (the number of payloads).
    
- **Best For:** Testing cases where you suspect the username and password might be identical, or when a value needs to be repeated in multiple headers.
    

### 3. Pitchfork

**The "Parallel" approach.**

Pitchfork uses **multiple payload sets** (one for each position). It moves through the lists in lockstep.

- **How it works:** It takes the first item from List A and the first item from List B and sends them together. Then it takes the second item from both, and so on.
    
- **Total Requests:** Equal to the size of the **smallest** payload set.
    
- **Best For:** Testing known pairs of data, such as a list of specific usernames and their corresponding known passwords.
    

### 4. Cluster Bomb

**The "Exhaustive" approach.**

This uses **multiple payload sets** and tests **every possible combination** (Cartesian product).

- **How it works:** It takes the first item from List A and pairs it with _every_ item in List B. Then it takes the second item from List A and pairs it with _every_ item in List B.
    
- **Total Requests:** $n \times m$ (Payload Set 1 size multiplied by Payload Set 2 size).
    
- **Best For:** Brute-forcing logins where you don't know which username belongs to which password.

### CSRF (Cross-Site Request Forgery)
![[img/3b370cfce8a050faf415c7d9a5a8227e.gif]]
![[img/sqdqdsqsd.gif]]
