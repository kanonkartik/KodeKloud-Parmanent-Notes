Below is a distilled version of the key concepts from My Jenkins learning experience, organized into a concise format that I  include in a permanent note. It covers the architecture, setup, troubleshooting, and project workflows—everything critical from I work. This can serve as a quick reference or foundation for future notes.

---



Date: March 04, 2025  
Topic: Jenkins Architecture, Setup, and Freestyle Projects  
Source: Hands-on tasks from Feb 2025 Jenkins learning session

---

1. Jenkins Architecture

- Controller Node: Central hub that manages jobs, created via CLI, UI, or APIs.
    
- Worker Nodes (Executors): Machines (Linux/Windows) that execute code, connected via:
    
    - SSH or JNLP (Java Network Launch Protocol).
        
    - Can leverage Docker or Kubernetes agents for scalability.
        
- Job Flow Example: Two jobs assigned by the controller to worker nodes for execution.
    

---

1. Hardware & Software Requirements

- Minimum:
    
    - CPU: 2 cores
        
    - RAM: 256 MB
        
    - Disk Space: 1 GB
        
- Recommended:
    
    - CPU: 4 cores
        
    - RAM: 4 GB
        
    - Disk Space: 50 GB
        
- Software:
    
    - Web browser for UI access.
        
    - JRE or JDK (JDK preferred for production).
        

---

1. Installation & Troubleshooting

- Initial Failure: Jenkins failed to start due to missing Java.
    
    - Check logs: sudo journalctl -xeu jenkins.service
        
    - Error: jenkins: failed to find a valid Java installation
        
    - Fix: Wrote error to /home/bob/failure.txt using echo 'jenkins: failed to find a valid Java installation' > failure.txt
        
- Install OpenJDK 17:
    
    - Commands:
        
        sh
        
        ```text
        sudo apt update
        sudo apt install fontconfig openjdk-17-jre -y
        java -version
        ```
        
    - Restart Jenkins: sudo systemctl restart jenkins
        
    - Verify: sudo systemctl status jenkins (Active/Running state).
        

---

1. Jenkins UI Setup

- Access: Port 8081.
    
- Unlock: Retrieve initial admin password:
    
    sh
    
    ```text
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```
    
- Plugins:
    
    - Dark Theme, Credentials Binding, Pipeline, Pipeline Graph View, Timestamper, Git, Pipeline: GitHub Groovy Libraries, GitHub Branch Source.
        
    - Install via "Manage Jenkins > Plugins" > Select > Install.
        
- User Config: Username: admin, Password: admin321.
    

---

1. Freestyle Projects

- Project 1: lab1-build-ascii-generator
    
    - Description: "Exploring Freestyle Projects"
        
    - SCM: None
        
    - Build Step: Execute shell:
        
        sh
        
        ```text
        curl -s https://api.adviceslip.com/advice -o advice.json
        cat advice.json
        ```
        
    - Later Modified:
        
        - Archive advice.json (Post-build Actions > Archive Artifacts > Enable "Only if build successful").
            
        - Allow lab1-test-and-deploy-ascii-generator to copy artifact.
            
- Project 2: lab1-test-and-deploy-ascii-generator
    
    - Description: "This job will always run after the lab1-build-ascii-generator job"
        
    - SCM: None
        
    - Build Trigger: Build after lab1-build-ascii-generator (Trigger only if stable).
        
    - Build Step: Execute shell:
        
        sh
        
        ```text
        cat /var/lib/jenkins/workspace/lab1-build-ascii-generator/advice.json | jq -r .slip.advice > ${WORKSPACE}/advice.message
        [ $(wc -w < ${WORKSPACE}/advice.message) -gt 5 ] && echo "Advice has more than 5 words" || (echo "Advice - $(cat ${WORKSPACE}/advice.message) has 5 words or less" && exit 1)
        cat ${WORKSPACE}/advice.message | /usr/games/cowsay -f $(ls /usr/share/cowsay/cows | shuf -n 1)
        ```
        
    - Initial Issue: Failed due to missing advice.json in its workspace.
        
    - Fix:
        
        - Install Copy Artifact Plugin (Manage Jenkins > Plugins > Copy Artifact).
            
        - Add Build Step: Copy artifacts from lab1-build-ascii-generator (Latest successful build, stable only, advice.json).
            
        - Reorder steps: Copy artifact first, then process.
            

---

1. Key Challenges & Lessons

- Java Dependency: Jenkins won’t run without a valid JDK/JRE—always verify with logs.
    
- Artifact Management: Archiving and copying files between jobs requires the Copy Artifact Plugin and proper configuration.
    
- Job Dependencies: Linking projects (e.g., triggering one job after another) needs precise trigger settings.
    
- File Paths: Workspace paths differ between jobs—adjust scripts or use artifacts to share files.
    

---

1. Commands Quick Reference

- Logs: sudo journalctl -xeu jenkins.service
    
- JDK Install: sudo apt install openjdk-17-jre -y
    
- Restart Jenkins: sudo systemctl restart jenkins
    
- Status: sudo systemctl status jenkins
    
- Admin Password: sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    

---

This note captures the essence of Jenkins’ architecture, I setup process, troubleshooting steps, and project configurations. It’s structured for easy reference and covers every important part of my  experience. 