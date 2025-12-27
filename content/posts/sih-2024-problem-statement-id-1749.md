---
title: "SIH 2024 Problem Statement ID-1749"
description: "A critical look at data recovery challenges in XFS and Btrfs, exploring misconceptions and highlighting effective recovery tools."
date: 2024-09-18T01:28:15+05:30
categories: ["Personal", "Opinions"]
tags: ["xfs", "btrfs", "file-systems", "linux", "hackathon-insights", "rants"]
draft: false
---

## Context

**For those who don't know about SIH** (Smart India Hackathon)
is conducted by the Indian Government every year.
This year i.e. 2024 , I found a problem statement to my liking
which is problem statement **ID: 1749**.
It is based on data recovery from XFS and BTRFS file systems,
which I have daily drive for quite extensively.

**For those who don't know about file systems (FS) in general** is file systems
are the type of systems that the user use to organize data inside the storage.
Then the storage is divided into partitions to manage large storage space.

There are various types of file systems ranging from:

- **FAT-32** commonly used in pendrives.
- **NTFS** used in Microsoft Windows for your (C,D,E etc local drives).
- **AFS** used in Apple MAC for local drives.
- Similarly, there is no fixed filesystem for Linux, there are options.
  Some popular ones are **Ext4**, **XFS**, **BTRFS**,**ZFS** and etc.

## What is the need for XFS or Btrfs when other filesystems already exist ?

1. **XFS** (1994):
   - High performance. The fastest file system which can be reliably used a computer.
   - It is backed by the largest Linux Powered Company
     **RHEL (Red Hat Enterprise Linux)**. RHEL uses XFS as it's default file system.
   - **Features**:
   - **Journaling**:
     XFS uses journal (specific file) to log metadata changes before they are committed.
     This ensures consistency and quick recovery in the event of a crash
     or power failure.
   - **CoW (Copy on Write)**:
     As the name suggests, copy on write is a feature that makes a copy of the file
     which is currently being written.
   - **Online Defragmentation**:
     This refers to defragmentation of the partition on the fly
     (without stopping everything and staring at the screen until the process ends)
     without halting current processes.
   - **Quota Support**:
     Provides support for user and group quotas to manage and limit disk usage.

2. **BTRFS** (2009):
   - High Stability and Scalablity.
   - Developed by SUSE, Meta, Western Digital, Oracle Corporation,
     Intel, The Linux Foundation, Red Hat.
   - SUSE uses it as it's default file system.
   - **Features**:
   - **CoW**
   - **Snapshots**:
     These are pictures (not actual pictures but states) of the file system
     at a particular time for the means of backup.
     These snapshots are used for restoring data.
   - **Subvolumes**: This functions similar to **Linux's
     LVM (Logical Volume Manager)** and helps to manage the whole storage
     into chunks of virtual volumes (virtual storage spaces).
   - **Data De-duplication**: Well, again the name defines itself.
     This feature helps to remove duplicate data from the file system.
   - **Data Scrubbing**: Not to be confused with "data cleaning", it
     checks for errors in the form of a background task.

> [!NOTE]
> All the features given here are not everything,
> but the most important ones which make them
> easily distinguishable from other file systems.

This should be enough for you understand what file systems are and what are the
features provided by file systems to manage and protect, user and system data.

## Analysis of the problem statement

### Addressing the "Challenges" section

**Challenges with Modern File Systems**:

1. Traditional file systems (like FAT and NTFS) are well-understood,
   and tools to recover deleted files from them are mature.
2. However, modern file systems like XFS and Btrfs are designed
   for better performance and reliability but are more complex,
   making data recovery harder.

**My thoughts**:

1. From data backup and recovery perspective:
   - **BTRFS** by default supports extensively in this matter.
   - **XFS** by default doesn't support data recovery options like snapshots,
     but due to its support for **CoW**, external snapshot tools can be
     used for data backups and restores.

2. From performance aspect:
   - **XFS** is designed to be very fast and very scalable.
   - **BTRFS** is not well designed for performance in mind.
     Some might argue that Btrfs is one of the slowest file system to ever exist.

> [!TLDR]
> So, the challenge here feels like a toddler throwing a tantrum because
> their toy does not come with a 🪄 magic button
> to operate all the fancy grown-up tools,
> as if the real problem is not having a flashy interface. 😂.
> Maybe next time they’ll want a touchscreen for their sandbox! 😆

### Addressing the "What's Needed" section

**What's needed**:

1. Recover Deleted Data Efficiently:
   - Challenge: Extracting deleted files from XFS and Btrfs
     can be tricky due to their complex structures.
   - Solution: Develop tools and techniques to locate and recover these files.

2. Support Various File Types:
   - Range of Files: The recovery solution should handle
     different types of files, including:
     - Documents: (e.g., .docx, .pdf, .txt)
     - Archives: (e.g., .zip, .tar)
     - Images: (e.g., .jpg, .png)
     - Executable: (e.g., .exe, .dll)
     - Scripts: (e.g., .sh, .py)
     - Databases: (e.g., .db)

3. Extract Complete Metadata:
   - What Metadata Includes: Information like when a file was created, last accessed, last modified, and deleted. This helps establish context and relevance for the investigation.

4. User-Friendly Interface:
   - Ease of Use: The solution should offer an easy-to-use interface (either graphical or command-line) for navigating recovered data and generating reports.

5. Ensure Data Integrity:
   - Data Validation: Ensure that the recovered data is accurate and hasn't been corrupted during the recovery process.

**My Thoughts**:

1. Recover Deleted Data Efficiently:
   - `xfs_undelete`.
   - `btrfs restore` using in conjunction with `btrfs-find-root`.

2. Handling different types of files:
   - Recovering a volume or partition leads to the recovery of the volume or the partition.
     Managing files and folders is a separate thing.

3. Metadata extraction:
   - `xfs_db` and `xfs_metadump`.
   - `btrfs inspect-internal` and `btrfs-debug-tree`.

4. > _Now, let’s dive into the part everyone’s secretly hoping I’ll rant about: “The G U I”.
   > Yes, that elusive “Graphical User Interface” that everyone seems to think is the Holy Grail of software.
   > It’s almost like folks believe a GUI will magically turn their problems into confetti!_ 🎉
   > Let’s get real sometimes, a sleek interface is just window dressing for the underlying magic of command-line tools.
   > So, grab your popcorn and let’s see why sometimes, fancy buttons don’t solve everything!\_ 🍿😂

**So here’s the scoop**: People often believe that a GUI is the golden ticket to ease and efficiency, as if slapping a few colorful icons on a screen will somehow simplify the complex task of data recovery.
Or Somehow a GUI can untangle the messy intricacies of **XFS** and **BTRFS** with a single, gleaming "Recovery All" Button! 😂
But let’s not kid ourselves.
A GUI is great for eye candy and accessibility, but it can’t perform miracles.

> _It’s like asking a toddler to drive a Ferrari.
> Sure, they might look cute in the driver’s seat, but they won’t get you very far._

Behind those flashy buttons and intuitive menus, there’s a whole world of command-line magic happening.
The real heavy lifting in data recovery isn’t about dragging and dropping; it’s about running the right commands with precision.
Command-line tools might seem less glamorous, but they’re where the real power lies.
They get into the nuts and bolts of the file system and can handle tasks with the kind of finesse that a GUI might struggle to replicate.

After all, it’s not all about the pretty interface; it’s about getting the job done.
And sometimes, those flashy GUIs are just a distraction from the real tools that can actually make a difference.
Next time, let’s not be fooled by the glitter; sometimes, the best solutions come with a black screen and a blinking cursor. 😎💻

5. Data Integrity:

- **XFS**
- **Journaling**
- **xfs_repair**
- **BTRFS**
- **CoW**
- **Checksumming**
- **Btrfs scrub**
  Best thing is these are the features of the file systems and natively available for use.

It’s really frustrating when people complain about data recovery being harder without acknowledging the powerful CLI tools specifically designed for these tasks.
The tools that were literally built for the job!
Instead of dismissing them, maybe it’s worth learning how to use them properly before blaming the file systems.

> Ignoring these tools and then crying foul is like complaining about not knowing how to cook while refusing to use a recipe book.
> Or like insisting your car doesn’t run well while stubbornly avoiding the owner's manual.
> It’s like saying you can’t bake a cake because you don’t have an oven, while standing right in front of one and asking for a microwave version! 🍰🔧

Instead of blaming the file systems, maybe it’s time to get acquainted with these command-line tools. After all, just because a recipe book doesn’t have a flashy cover doesn’t mean it won’t make you the best cake in town! 🎂💻

## Conclusion

At the very least, they should stop spewing nonsense in their problem statements.
Complaining about data recovery being hard while ignoring powerful CLI tools is like bemoaning a broken sink while staring at the toolbox.
It’s almost as if they’re deliberately ignoring the solution and then playing the victim-classic move!

In reality, both XFS and Btrfs have their strengths, and while they may introduce complexities, they also come equipped with powerful tools for tackling data recovery.
Relying solely on a flashy GUI might seem like the easy route, but the real magic happens with those gritty command-line tools that get into the nuts and bolts of recovery.
So, rather than blaming the file systems, maybe it’s time to roll up our sleeves, learn those CLI commands, and get the job done.
After all, mastering the command line isn’t about having the shiniest interface; it’s about wielding the true power of data recovery.
Let's stop playing the victim and start appreciating the tools that were literally made for this job!
