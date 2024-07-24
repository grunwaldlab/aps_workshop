# PathogenSurveillance workshop

This session is part of [**Nanopore Sequencing and Whole Genome Assembly and Annotation with nf-core/pathogensurveillance**](https://events.rdmobile.com/Sessions/Details/2316143)

---

### **Table of Content**

### **⚙️ Resources**

[https://github.com/grunwaldlab/pathogensurveillance](https://github.com/grunwaldlab/pathogensurveillance)

[https://github.com/grunwaldlab/psminer](https://github.com/grunwaldlab/psminer)

<aside>
🚧 **OUTLINE**

Part 1 Setting up [gitpod](https://www.gitpod.io/) [¶](https://www.notion.so/PathogenSurveillance-workshop-f630b9c1dc204bb7acd3cee19e16b522?pvs=21)

Part 2 

</aside>

- **🦤 Session leader(s) bios**
    
    
    **Zach Foster**
    
    ![Untitled](content/Untitled.png)
    
    **Alex Weisberg**
    
    ![Untitled](content/Untitled%201.png)
    
    **Camilo H. Parada Rojas**
    
    ![Untitled](content/Untitled%202.png)
    
    **Jeff Chang**
    
    ![Untitled](content/Untitled%203.png)
    
    **Martha Sudermann**
    
    ![Untitled](content/Untitled%204.png)
    
    **Nik Grunwald**
    
    ![Untitled](content/Untitled%205.png)
    

---

# **🧰 Prerequisites**

- **Some familiarity with the linux command-line interface if not look here for resources.**
    
    https://open.oregonstate.education/computationalbiology/chapter/the-command-line-and-filesystem/
    
    [PCfB_Appendices.pdf](content/PCfB_Appendices.pdf)
    
- **Github account, if you don't have one, please get one at [github.com](http://github.com)**
    
    https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github
    
- **Understanding of genomic terms**
    
    reads
    
    genome
    
    populations
    
    contigs
    
    annotations
    
    phylogenies
    
    variants/SNPs
    
    homology
    
- **Understanding of the need for bioinformatics workflows**
    
    
- **Understand the general role and input/output files**
    
    

# 1) Setting up [gitpod](https://www.gitpod.io/) [¶](https://www.notion.so/PathogenSurveillance-workshop-f630b9c1dc204bb7acd3cee19e16b522?pvs=21)

## What is Gitpod?

We are using *Gitpod* to provide hands-on experience of installing and using the pathogen surveillance pipeline we developed. [**Gitpod**](https://gitpod.io/) allows you to launch and enter Virtual Machines from your browser and gives you 50 free hours per calendar month, enough for this session. 

## How do I sign up for Gitpod?

You MUST do the following steps before the workshop starts! It will take a few minutes each to set up a **GitHub** account and to set up a **Gitpod** account if you don't already have them:

**STEP 00** ~ Click on [https://gitpod.io/new#https://github.com/grunwaldlab/aps_workshop](https://gitpod.io/new#https://github.com/grunwaldlab/aps_workshop) in any desktop web browser (**Note: Safari sometimes has problems on a Mac, so use Chrome or Mozilla instead)**

![Untitled](content/Untitled%206.png)

**STEP 01 ~** It will ask you to sign up with a GitHub account. If you don't have one, please get one at https://github.com/

![Untitled](content/Untitled%207.png)

**STEP 02 ~** Once you are signed in to gitub.com - click on the gitpod.io link above again. It will try to launch a our Gitpod workspace using your GitHub login. You will need to give Gitpod permission to access (only) the email address on your GitHub account. Follow the Gitpod prompts to ensure you are a real human and won't misuse their resources. **Note: if it asks you to connect your LinkedIn, you can skip that - you will still get 50 hours :-)**

**STEP 03 ~** Gitpod will ask you to select which code editor and which machine size to start. The defaults are fine. So just click **Continue**

![Untitled](content/Untitled%208.png)

**STEP 04 ~** Once the Gitpod workspace starts (typically in less than a minute), you will see the following in your desktop web browser: a file browser on your left, a text editor top right, and a linux terminal bottom right.

![Untitled](content/Untitled.jpeg)

> *If you are doing this before the workshop, please go to [gitpod.io/workspaces](https://gitpod.io/workspaces) to delete any running workspaces (in green) so that you don't use up your 50 hours per month* 🙂
>
