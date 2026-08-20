# Day 08 - Git and GitHub Fundamentals


### 1. Version Control System

A **Version Control System (VCS)** is a tool that records changes made to files over time. It allows individuals and teams to manage source code, preserve different versions, review modifications, and restore earlier working states when necessary.

Version control primarily solves two problems:

1. **Code sharing and collaboration**
2. **Versioning and change history**

#### 1.1 Code Sharing and Collaboration

Consider two developers building the same calculator application:

- Developer 1 implements the **addition** functionality.
- Developer 2 implements the **subtraction** functionality.
- Both changes must eventually become part of one application.

Exchanging files through email or chat may appear sufficient for a tiny project, but it does not scale. A production application may contain hundreds of packages, thousands of files, and many dependencies. Different developers may modify dozens of related files at the same time.

A VCS provides a common, controlled workflow in which developers can:

- Share code changes.
- Combine work from multiple contributors.
- Identify who changed a file.
- Maintain an organized project history.
- Avoid manually exchanging complete project folders.

#### 1.2 Versioning and Change History

Software requirements change continuously. For example, an addition function may evolve through several versions:

- Version 1: addition of two numbers.
- Version 2: addition of three numbers.
- Version 3: addition of four numbers.

If the newer behavior is no longer required, the team may need to return to Version 1. Manually recreating old code is unreliable, especially when changes span many files.

A VCS preserves recorded versions so that a team can:

- Examine earlier changes.
- Compare the current files with a previous state.
- Identify the change introduced on a particular date.
- Restore a known working version.
- Retain an auditable history of development.

In Git, a recorded version is represented by a **commit**.

---

### 2. Centralized and Distributed Version Control

Version control systems can use either a **centralized** or a **distributed** architecture.

#### 2.1 Centralized Version Control System

In a **Centralized Version Control System (CVCS)**, the authoritative repository and its history are maintained on a central server. Developers communicate through that server to share their work.

Examples discussed:

- **CVS**
- **SVN (Subversion)**

Typical workflow:

1. A developer sends changes to the central server.
2. Another developer retrieves those changes from the same server.
3. Shared repository operations depend on the availability of that server.

The central server can become a major dependency. If it is unavailable, developers may be unable to retrieve history or exchange changes through the normal workflow.

#### 2.2 Distributed Version Control System

In a **Distributed Version Control System (DVCS)**, every normal repository clone contains the project files and repository history. Developers can record commits and inspect history locally, then exchange changes through a shared remote repository when required.

**Git** is a distributed version control system.

Important characteristics include:

- Each developer can maintain a complete local repository.
- Local history operations do not require constant access to a central server.
- Developers can create commits while offline.
- Multiple copies of the repository reduce dependence on one physical copy of the history.
- A remote service such as GitHub can still be used as the team's common collaboration point.

If the shared remote is unavailable, developers cannot push or retrieve new remote changes until it recovers, but they can continue many local Git operations.

#### 2.3 Centralized vs. Distributed Version Control

| Aspect | Centralized VCS | Distributed VCS |
|---|---|---|
| Repository history | Primarily maintained on a central server | Present in every normal clone |
| Local commits | Usually depend more heavily on server access | Can be created locally |
| Offline work | Limited | Most history and commit operations remain available |
| Server outage | Can block normal history and collaboration operations | Blocks synchronization, but local work can continue |
| Copies of history | Primarily centralized | Distributed among repository clones |
| Examples | CVS, SVN | Git |

Git is widely adopted because its distributed design provides fast local operations, flexible collaboration, and better resilience than workflows that rely entirely on one central repository server.

---

### 3. Repository Copies, Clones, and Forks

A **repository copy** allows development to continue independently from another copy of the same project.

Two related concepts should not be confused:

- A **clone** is a local copy of a Git repository, normally containing the files and complete history.
- A **fork** is a server-side copy of a repository created under another account or namespace on a hosting platform such as GitHub.

A fork is useful when a developer wants to:

- Maintain an independent copy of a repository.
- Experiment without modifying the original repository directly.
- Collaborate using a repository under their own account.
- Retain access to their copy even when the original repository is temporarily unavailable, subject to the hosting service being available.

A fork is a feature supplied by platforms such as GitHub; it is not a separate Git version-control architecture.

---

### 4. Git and GitHub

Git and GitHub are related, but they are not the same product.

#### 4.1 Git

**Git** is an open-source, distributed version control system. It is installed on a developer's machine or organizational infrastructure and is used to:

- Initialize repositories.
- Track selected files.
- Stage changes.
- Create commits.
- Compare modifications.
- View history.
- Move between recorded versions.

An organization can host Git repositories on its own infrastructure, including Linux servers or cloud virtual machines.

#### 4.2 GitHub

**GitHub** is a hosted collaboration platform built around Git repositories. It provides services beyond Git's core version-control commands, including:

- Remote repository hosting.
- A web-based user interface.
- User and access management.
- Code review and team collaboration.
- Issue tracking and discussions.
- Project-management features.
- Repository forking.
- Security and automation capabilities.

Other platforms based on Git include **GitLab** and **Bitbucket**.

#### 4.3 Git vs. GitHub

| Git | GitHub |
|---|---|
| A distributed version control system | A hosted platform for Git repositories |
| Installed and used locally | Accessed as a remote service and web application |
| Tracks files, commits, branches, and history | Adds hosting, permissions, collaboration, issues, reviews, and project features |
| Can work without GitHub | Depends on Git repositories for its core source-control workflow |
| Open-source version-control software | A commercial platform with public and private hosting options |

Git can be used without GitHub. GitHub makes it easier to host, share, and collaborate on Git repositories.

---

### 5. Creating a Local Git Repository

#### 5.1 Install and Verify Git

Git must be installed before its commands can be used. Installation packages are available for Linux, Windows, and macOS.

Running the following command displays Git's available commands and confirms that the executable is available:

```bash
git
```

#### 5.2 Create a Project Directory

The example project uses a directory named `example.com` and a file named `calculator.sh`:

```bash
mkdir example.com
cd example.com
vim calculator.sh
```

The calculator file initially represents a simple addition operation.

#### 5.3 Initialize the Repository

Run the following command from the project directory:

```bash
git init
```

`git init` creates an empty Git repository by adding a hidden `.git` directory. The existing project files are not automatically committed merely because the repository has been initialized.

To display hidden files and verify that `.git` exists:

```bash
ls -la
```

---

### 6. The `.git` Directory

The `.git` directory contains the repository's metadata and history. Git uses it to determine the current state of the project and to compare the working files with recorded versions.

Important contents include:

| Entry | Purpose |
|---|---|
| `objects/` | Stores Git objects that represent file content, directory structures, and commits |
| `refs/` | Stores references to branches, tags, and other named commit pointers |
| `hooks/` | Contains hook scripts that can run checks or automation around Git actions |
| `config` | Stores repository-specific configuration, such as remote and behavior settings |
| `HEAD` | Identifies the currently checked-out branch or commit |

Git hooks can be used to detect undesirable changes, such as accidentally staging passwords, API tokens, or other sensitive data. They are a preventive control and should be combined with secure development practices.

Raw credentials and secrets should not be stored in repository files or committed to Git.

> **Important:** Deleting `.git` removes the local repository metadata and history from that directory. The ordinary project files may remain, but Git will no longer recognize the directory as the same tracked repository.

---

### 7. Git File States

A file moves through several states during the Git workflow:

| State | Meaning |
|---|---|
| **Untracked** | The file exists in the working directory, but Git has not been instructed to track it |
| **Modified** | A tracked file differs from its last recorded or staged state |
| **Staged** | The current version of the file has been selected for the next commit |
| **Committed** | The staged version has been stored in the local repository history |
| **Clean working tree** | No tracked changes are waiting to be staged or committed |

The main lifecycle is:

| Location or stage | Main action | Relevant command |
|---|---|---|
| Working directory | Create or modify files | Editor such as `vim` |
| Inspection | Check state and review modifications | `git status`, `git diff` |
| Staging area | Select content for the next commit | `git add` |
| Local repository | Record a version | `git commit` |
| Remote repository | Share local commits | `git push` |

---

### 8. Inspecting Repository Status

Use the following command frequently:

```bash
git status
```

`git status` reports information such as:

- The current branch.
- Untracked files.
- Modified files.
- Changes staged for commit.
- Changes not yet staged.
- Whether the working tree is clean.

After `calculator.sh` is created, Git initially reports it as an untracked file.

---

### 9. Staging Files with `git add`

To begin tracking a file and stage its current content:

```bash
git add calculator.sh
```

`git add` does not permanently record a version by itself. It places the selected content in the **staging area**, preparing it for the next commit.

After staging, run `git status` again to confirm what will be included in the commit.

---

### 10. Reviewing Changes with `git diff`

After modifying a tracked file, use:

```bash
git diff
```

`git diff` displays the unstaged differences between the working directory and the current staged or recorded state. For example, it can show that:

```text
x = a + b
```

was changed to:

```text
x = a + b + c
```

Reviewing the diff before staging helps confirm that only the intended code was changed.

---

### 11. Recording Versions with `git commit`

A **commit** records the staged project state in the local Git history.

```bash
git commit -m "Add initial addition functionality"
```

The `-m` option supplies a commit message. A useful commit message should explain the purpose of the recorded change.

A clean workflow for a second change is:

```bash
git diff
git add calculator.sh
git status
git commit -m "Add subtraction functionality"
```

After a successful commit, `git status` may report:

```text
nothing to commit, working tree clean
```

This means Git detects no uncommitted tracked changes at that moment.

---

### 12. Viewing Commit History

Use the following command to display repository history:

```bash
git log
```

The log normally includes:

- A unique commit identifier.
- Author information.
- Date and time.
- Commit message.

The commit identifier is commonly called a **commit ID**, **commit hash**, or **SHA**. It can be used to identify a specific recorded version.

---

### 13. Returning to an Earlier Commit

First, locate the required commit ID:

```bash
git log
```

The following command moves the current branch and working tree to an earlier commit:

```bash
git reset --hard <commit-id>
```

The file can then be inspected:

```bash
cat calculator.sh
```

#### Important Safety Warning

`git reset --hard` is destructive to uncommitted working-directory and staged changes. It also moves the current branch pointer. Before using it:

- Confirm the target commit ID.
- Check `git status`.
- Preserve any work that must not be lost.
- Avoid rewriting shared history without understanding the effect on other contributors.

The command demonstrates Git's ability to restore an earlier recorded state, but it should be used carefully.

---

### 14. Local and Remote Repositories

The repository created with `git init` exists only on the local machine. Local commits provide versioning, but they are not automatically available to teammates.

To share the repository, a team can use:

- GitHub.
- GitLab.
- Bitbucket.
- A self-hosted Git service.

The shared repository is commonly called a **remote repository**. After it is configured, `git push` sends local commits to it.

```bash
git push
```

The exact remote setup and push syntax depend on the repository configuration.

---

### 15. Creating a Repository on GitHub

The general GitHub repository-creation process is:

1. Create or sign in to a GitHub account.
2. Select **New repository**.
3. Enter a repository name.
4. Add an optional description.
5. Choose the repository visibility.
6. Optionally initialize it with a `README` file.
7. Select **Create repository**.

> **Common setup consideration:** If an existing local repository already contains commits, initializing the new remote with a README creates a separate remote commit. The simplest first-push setup is usually an empty remote; otherwise, the remote commit must be retrieved and integrated before the histories are synchronized.

#### 15.1 Public and Private Repositories

| Visibility | Meaning |
|---|---|
| **Public** | The repository can be viewed by anyone with access to the public hosting service |
| **Private** | The repository is limited to the owner and explicitly authorized users or teams |

Choose visibility according to the sensitivity of the source code and the organization's access policy.

#### 15.2 README File

A `README` provides introductory information about the repository, such as:

- Project purpose.
- Supported functionality.
- Setup or usage instructions.
- Important project metadata.

For the calculator example, the README could explain that the shell script provides addition and subtraction operations.

#### 15.3 Adding Code to the GitHub Repository

Code can be added in two general ways:

- Push an existing local Git repository to GitHub.
- Create or edit files directly through GitHub's web interface.

Once the remote repository contains the code, authorized developers can access it and collaborate. A developer may also create a fork under their own GitHub account.

---

### 16. End-to-End Git Workflow

A beginner-friendly local workflow is:

```bash
# Create and enter the project directory
mkdir example.com
cd example.com

# Create or edit a project file
vim calculator.sh

# Initialize the local repository
git init

# Confirm the repository and inspect file state
ls -la
git status

# Stage the file
git add calculator.sh
git status

# Record the first version
git commit -m "Add initial addition functionality"

# Modify and inspect the file
vim calculator.sh
git status
git diff

# Stage and record the next version
git add calculator.sh
git status
git commit -m "Add subtraction functionality"

# Inspect repository history
git log
```

After a remote repository has been configured, local commits can be shared with:

```bash
git push
```

---

### 17. Recommended Working Practices

- Run `git status` frequently to understand the repository state.
- Review changes with `git diff` before staging them.
- Stage only the files intended for the next commit.
- Use concise and meaningful commit messages.
- Create commits that represent clear, logical changes.
- Do not delete the `.git` directory unintentionally.
- Never commit passwords, API tokens, certificates, or other secrets.
- Use hooks or security checks to detect sensitive content before it is committed.
- Treat `git reset --hard` as a destructive command.
- Add a clear README when publishing a repository.
- Select public or private visibility according to the project's access requirements.

## Interview Questions and Answers

### 1. What is a Version Control System?

A Version Control System records changes to files over time so users can collaborate, inspect history, compare versions, and restore earlier states.

### 2. What two major problems does version control solve?

It solves **code sharing and collaboration** and **versioning or change-history management**.

### 3. Why is manually sharing source files through email unsuitable for large projects?

Large projects contain many interdependent files modified by multiple people. Manual sharing makes it difficult to combine changes, preserve history, identify ownership, and avoid missing or overwriting files.

### 4. What is versioning?

Versioning is the process of preserving identifiable states of a project so that changes can be reviewed and an earlier state can be restored when required.

### 5. What is a centralized version control system?

A centralized VCS maintains the authoritative repository and history on a central server through which developers normally exchange changes.

### 6. What is a distributed version control system?

A distributed VCS gives each normal clone a complete repository, including its history, allowing developers to commit and inspect history locally before synchronizing with others.

### 7. What is the main difference between centralized and distributed version control?

A centralized system primarily depends on one server for repository history, whereas a distributed system places a full repository copy and history in each normal clone.

### 8. Give examples of centralized and distributed version control systems.

CVS and SVN are centralized systems. Git is a distributed version control system.

### 9. Why can a central server become a single point of failure in a CVCS workflow?

If the central server becomes unavailable, developers may be unable to access repository history or exchange changes through the standard workflow.

### 10. Can Git users continue working if the shared remote repository is temporarily unavailable?

Yes. They can edit files, inspect local history, stage changes, and create local commits. They cannot synchronize new changes with the unavailable remote until it recovers.

### 11. Why did Git become popular?

Git provides distributed history, fast local operations, offline commits, flexible collaboration, and reduced dependence on one central repository copy.

### 12. What is the difference between Git and GitHub?

Git is a distributed version control system. GitHub is a hosted platform that stores Git repositories and adds collaboration, access control, issue tracking, reviews, project features, and automation.

### 13. Can Git be used without GitHub?

Yes. Git can operate entirely locally or use a self-hosted or alternative remote service such as GitLab or Bitbucket.

### 14. What is a Git repository?

A Git repository is a project directory whose versions and metadata are managed by Git through its `.git` directory.

### 15. What does `git init` do?

It initializes a new Git repository in the current directory by creating the hidden `.git` metadata directory.

### 16. What is stored inside the `.git` directory?

It stores repository history, objects, references, configuration, hooks, `HEAD`, and other metadata Git needs to manage the repository.

### 17. What happens if the `.git` directory is deleted?

The project files normally remain, but the local Git history and repository metadata in that directory are removed, so Git no longer recognizes it as the same repository.

### 18. What are Git objects?

Git objects are internal data structures used to store file content, directory structures, commits, and related repository information.

### 19. What are Git references?

References are named pointers to commits, including branch and tag references.

### 20. What are Git hooks?

Git hooks are scripts triggered around Git actions. They can automate checks, such as detecting sensitive data before a commit is accepted locally.

### 21. What is `HEAD` in Git?

`HEAD` identifies the currently checked-out branch or commit and represents the developer's current position in repository history.

### 22. What is an untracked file?

An untracked file exists in the working directory but has not yet been added to Git's tracking workflow.

### 23. What is the purpose of `git status`?

It displays the current branch and the state of untracked, modified, staged, and committed content in the working tree.

### 24. What does `git add` do?

It stages the current content of one or more files for inclusion in the next commit. It does not create the commit itself.

### 25. What is the purpose of `git diff`?

It displays unstaged changes so a developer can review how working files differ from the current staged or recorded state.

### 26. What is a Git commit?

A commit is a recorded snapshot of staged project content, identified by a unique hash and accompanied by metadata such as the author and message.

### 27. What information does `git log` provide?

It shows commit history, including commit IDs, authors, dates, and commit messages.

### 28. What does `git reset --hard <commit-id>` do?

It moves the current branch to the specified commit and forces the staging area and working tree to match it. Uncommitted changes can be permanently lost.

### 29. What is a fork?

A fork is a server-side copy of a repository under another account or namespace on a hosting platform, allowing independent development and collaboration.

### 30. What is the purpose of `git push`?

`git push` transfers local commits and reference updates to a configured remote repository so that the changes can be shared.

## Scenario-Based Interview Questions

### 1. Two developers are exchanging dozens of modified files through email, and their changes frequently overwrite each other. What would you recommend?

Use a version control system such as Git and a shared remote repository. Each developer should record logical commits locally and synchronize them through the remote instead of exchanging complete folders manually.

### 2. The team's GitHub repository is temporarily unavailable. Can developers continue working?

Yes. Because Git is distributed, developers can edit files, run `git status` and `git diff`, and create local commits. Push and retrieval of new remote changes must wait until the service becomes available again.

### 3. A new file appears under "Untracked files" in `git status`. How do you include it in the next version?

Review the file, run `git add <file-name>` to stage it, verify the staging result with `git status`, and then create a commit with a meaningful message.

### 4. A developer wants to verify exactly what was changed before creating a commit. Which commands should be used?

Run `git status` to identify modified files and `git diff` to inspect the unstaged line-level changes. Stage the intended file only after reviewing it.

### 5. A tracked file was modified, but `git log` does not show a new version. Why?

Modifying a file does not automatically create a version. The developer must stage the change with `git add` and record it with `git commit` before it appears in the commit history.

### 6. A project owner asks you to return a local branch to a known earlier commit. What should you check before using a hard reset?

Use `git log` to verify the commit ID and `git status` to check for uncommitted work. Preserve any required changes before running `git reset --hard <commit-id>`, because the command discards staged and working-tree changes and moves the branch pointer.

### 7. A developer accidentally deletes the `.git` directory. What is the impact?

The working files may still exist, but the directory loses its local Git metadata and history. If a remote copy exists, the normal recovery is to obtain the repository again from that trusted source; simply running `git init` creates a new history rather than restoring the old one.

### 8. A team repeatedly attempts to commit API tokens. How can Git hooks help?

A pre-commit hook can scan staged content and reject a commit when it detects likely credentials. The team must still remove exposed secrets, rotate compromised tokens, and avoid storing credentials in tracked files.

### 9. An organization wants only approved employees to view a repository. Should it be public or private?

It should be private, with access granted only to authorized users or teams according to the organization's security policy.

### 10. A developer wants an independent GitHub copy of another repository under their own account. What should they create?

They should create a fork. The fork provides a server-side repository in their namespace where they can maintain independent changes without directly modifying the original repository.

### 11. A local repository contains several commits, but teammates cannot see them on GitHub. What is missing?

Local commits are not automatically uploaded. The repository must have an appropriate remote configuration, and the commits must be shared using `git push`.

### 12. `git status` reports "nothing to commit, working tree clean." What does this indicate?

It indicates that Git currently detects no tracked working-directory or staged changes waiting to be committed. Untracked ignored content may still exist depending on repository settings, but no ordinary pending tracked change is reported.

## Quick Revision Notes

- A **VCS** manages file changes, collaboration, and version history.
- Version control solves **code sharing** and **versioning** problems.
- Emailing source files does not scale for multi-file, multi-developer projects.
- **CVS** and **SVN** are centralized version control systems.
- **Git** is a distributed version control system.
- Every normal Git clone contains repository history.
- A remote outage prevents synchronization but does not stop most local Git work.
- A **fork** is a platform-hosted copy under another account or namespace.
- **Git** manages source history; **GitHub** hosts Git repositories and adds collaboration features.
- `git init` creates a local repository and its `.git` directory.
- `.git` contains objects, references, hooks, configuration, `HEAD`, and history metadata.
- `git status` shows the repository's current file states.
- `git add` stages content for the next commit.
- `git diff` shows unstaged modifications.
- `git commit -m "message"` records staged content locally.
- `git log` displays commit history and commit IDs.
- `git reset --hard <commit-id>` restores a selected state destructively and must be used carefully.
- `git push` shares local commits with a configured remote repository.
- A README explains a repository's purpose, functionality, and usage.
- Public repositories are widely visible; private repositories require authorization.

## Key Terms and Definitions

| Term | Definition |
|---|---|
| **Version Control System (VCS)** | Software that records and manages changes to files over time |
| **Versioning** | Preserving identifiable project states so changes can be reviewed or restored |
| **Centralized VCS** | A VCS in which the main repository and history reside on a central server |
| **Distributed VCS** | A VCS in which each normal clone contains a complete repository and history |
| **Git** | An open-source distributed version control system |
| **GitHub** | A hosted Git repository and collaboration platform |
| **Repository** | A project and the version-control metadata used to track it |
| **Working directory** | The checked-out project files a developer currently edits |
| **Staging area** | The prepared set of file content that will be included in the next commit |
| **Untracked file** | A file present in the project directory that Git has not started tracking |
| **Modified file** | A tracked file whose current content differs from its staged or committed state |
| **Commit** | A recorded snapshot of staged project content and its metadata |
| **Commit ID / Hash / SHA** | The unique identifier associated with a Git commit |
| **Working tree clean** | A state in which no tracked modifications are waiting to be staged or committed |
| **`.git` directory** | The hidden directory containing local repository history and metadata |
| **Git object** | An internal object used to store content, directory structures, and commit data |
| **Reference (`ref`)** | A named pointer to a commit, such as a branch or tag |
| **HEAD** | The pointer representing the currently checked-out branch or commit |
| **Git hook** | A script triggered around a Git operation to perform checks or automation |
| **Remote repository** | A repository hosted elsewhere and used to exchange changes |
| **Fork** | A server-side copy of a repository under another account or namespace |
| **Clone** | A local copy of a Git repository, normally including its complete history |
| **README** | A file containing the project's overview, setup, usage, and supporting information |
| **Public repository** | A repository visible to the public according to the hosting platform's rules |
| **Private repository** | A repository accessible only to explicitly authorized users or teams |

## Important Commands

| Command | Purpose |
|---|---|
| `git` | Displays Git usage information and available commands; also helps verify that Git is installed |
| `mkdir example.com` | Creates the example project directory |
| `cd example.com` | Enters the project directory |
| `vim calculator.sh` | Creates or edits the example shell-script file in Vim |
| `git init` | Initializes a new local Git repository in the current directory |
| `ls -la` | Lists all directory entries, including the hidden `.git` directory |
| `git status` | Displays the current branch and the state of tracked, untracked, modified, and staged files |
| `git add calculator.sh` | Starts tracking or stages the current content of `calculator.sh` |
| `git add <file-name>` | Stages the specified file for the next commit |
| `git diff` | Shows unstaged changes in tracked files |
| `git commit -m "<message>"` | Records staged content in the local repository with a commit message |
| `git log` | Displays commit history, commit IDs, authors, dates, and messages |
| `git reset --hard <commit-id>` | Moves the current branch, staging area, and working tree to a selected commit; discards uncommitted changes |
| `cat calculator.sh` | Prints the file content to verify the restored version |
| `git push` | Sends local commits to a configured remote repository |

## Key Takeaways

- Git provides a distributed and reliable way to manage source-code history and team collaboration.
- The basic Git lifecycle is **modify → inspect → stage → commit → push**.
- `git status`, `git diff`, `git add`, `git commit`, and `git log` are the essential commands for everyday local work.
- Git and GitHub serve different purposes: Git performs version control, while GitHub hosts repositories and adds collaboration features.
- The `.git` directory is critical because it stores the repository's metadata and history.
- Commits make earlier project states identifiable and recoverable.
- Destructive commands such as `git reset --hard` require careful verification before use.
- Remote repositories make local Git history shareable, while forks allow independent server-side copies for collaboration.
