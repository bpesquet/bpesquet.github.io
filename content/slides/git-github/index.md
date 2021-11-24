---
title: "Git & Github"
date: 2021-11-23T19:01:29+01:00
draft: true
---

## Git

---

### The need for source code management

- Source code is the core of any software project.
- These projects have a long lifespan, with numerous releases containing new functionalities and bug fixes.
- Throughout this lifespan, the development team needs a way to work in parallel while sharing a common code base.

---

### Manual source code management

- Relies on shared places (local or cloud-based) where snapshots of the code base are regularly pushed by developers.
- Highly impractical: no individual history of files, no release management, no handling of conflicts (simultaneous updates of a file)...

---

### Version Control Systems

Dedicated source code management tools, often called **Version Control Systems**, offer developers the ability to:

- share and update a common code base;
- work on new features and fixes without breaking current versions;
- track who did what;
- handle conflicts;
- and more!

---

{{% section %}}

### Centralized VCS

- Uses only one repository, accessed by developers in a client/server way.
- Repo administration (security, backups...) is easy.
- Synchronization is impossible in a disconnected scenario.
- Examples: CVS, SVN, ClearCase.

---

![Centralized SCM](images/scm_centralized.png)

{{% /section %}}

---

{{% section %}}

### Decentralized VCS

- Each developer has its own code repository, including history and all other metadata.
- Repositories are frequently synchronized.
- Disconnected workflows become possible.
- Examples: Git, Mercurial.

---

![Decentralized SCM](images/scm_decentralized.png)

{{% /section %}}
