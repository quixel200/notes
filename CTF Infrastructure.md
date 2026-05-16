
# Objectives 

- An educational platform for learners to develop cybersecurity skills in a hands-on fashion.
- Each module will require the learner to apply the knowledge learnt in order to retrieve flags to complete the challenges.
- learn cybersecurity by diving deep into the core of computing, using that journey to absorb cybersecurity concepts.

# Outcomes 

- Learn necessary skills required by the cybersecurity industry including linux mastery, deep systems understanding, scripting and automation that serve as a foundation for further learning. 
- Bridge the gap between academic concepts (read in articles/videos) and practical execution, cementing knowledge through immediate application in a live environment
- Learn to analyze and exploit unique, randomized instances, ensuring that skills are transferable to real-world scenarios rather than reliant on static, memorized answers.
- equip the learner with the ability to participate in various CTF competitions including hirings CTFs.




- The platform will contain multiple "dojos", which will cover a range of topics.
![[Pasted image 20260108081815.png]]
- These dojos consist of modules each focusing on a single topic.
![[Pasted image 20260108081844.png]]
- These modules can include articles/videos allowing the student to learn. 
- These lecture videos are followed by challenges. 
![[Pasted image 20260108081920.png]]
- Each challenge spawns an instance that is unique to the user. 
- The flag is also generated randomly based on the username and the challenge, discouraging flag sharing 
- Each challenge can also contain multiple binaries assigning random challenges to each user.

- Solving an entire dojo will award the player with a badge that will be displayed on their profile, incentivising learning. 
![[Screenshot 2025-12-26 153005.png]]

# Instance details
- Each user gets their own VM with a persistent home directory, any work saved in the home directory will persist between challenges.

- The flag will be generated in /flag and all the relevant challenge files are located in /challenge 

- The user can either use the browser terminal, a code browser, a direct connection to the desktop, or an ssh connection to connect to the challenge.

- Each dojo also has weekly, monthly and all time leaderboards that update based on the solve time and the number of challenges solved.

