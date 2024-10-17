# Spring boot example project for beginners

## Introduction
This project is meant as a brief introduction into java/spring world for complete beginners that are only familiar with basics of java.
It should lead you step-by-step through the process of setting up and writing simple application with REST API and database storage.

*Following guide will be focused on MacOS and IntelliJ Idea.*

## Prerequisites
Download and install good IDE. [IntelliJ IDEA](https://www.jetbrains.com/idea/) is the best option, but does not support Spring in free version. [Visual Studio Code](https://code.visualstudio.com/) is also very good option.

Download and install latest version of Java. I recommend [Eclipse Temurin](https://adoptium.net/temurin/releases/) as it has open license and is backed by trusted organisation.

Download and install [Docker Desktop](https://www.docker.com/). This will extremely simplify the initial set up of 3rd party dependencies, as postgresql.

*Note - Docker is container engine that allows user to run various "prepackaged" applications without need to install them on local machine.
Docker (or similar technologies) is widely used in all environments and helps to mitigate large amount of environment-specific issues. It's **really** a good idea to get familiar with docker.*

## Generate project skeleton
To start with development of spring application, you should generate skeleton of the application using [Spring initializr](https://start.spring.io).

Here, simple gui can give you head start into the world of spring-based application

On the left side, there is basic project settings. On the image below is recommended settings for beginners, so it's easy to start with the implementation.

![Spring initializr project settings](assets/spring-initializr-settings.png "Recommended project settings for beginners")

- Maven is the simplest project management tool, more declarative than gradle and easier to understand and configure.
- Spring boot version should always be set to the newest available release.
- Packaging should always be set to `Jar`
  - Application packaged with `.jar` has built-in application server, which simplifies both initial setup and application deployment.
  - `.war` packaging is intended for deployment to standalone application server, which is more difficult to set up and deploy.
- Java should be always set to the newest available LTS Java release

![Spring initializr dependencies](assets/spring-initializr-dependencies.png "Recommended dependencies for beginners")

- Spring Boot DevTools is package that provides various QoL features during development.
- Spring Web is library for building web applications. Contains Tomcat embedded application server (allows the application to be started without external application server).
- Spring Data JDBC provides tools for communication with database
- MariaDB Driver is driver for specific database engine ([MariaDB](https://mariadb.org/), easy-to-use SQL database engine with open source license)

After you click on **GENERATE** button, the project will be generated into `.zip` file. Download and extract the `.zip` file.

## Set up GitHub access from command line
To enable GitHub access from command line, SSH key needs to be generated and assigned to GitHub account.

### Generating SSH key
Open `Terminal` application and put following commands to generate new ssh key

```shell
cd ~/.ssh
ssh-keygen -t ed25519 -f github -C "your_email@example.com" # Replace with your email
```
When asked for passphrase, confirm empty passphrase twice to create unencrypted record.

After the key is generated, run following command to copy public key of newly created key into clipboard:

```shell
cd ~/.ssh
cat github.pub | pbcopy
```

Go to [GitHub SSH keys setup](https://github.com/settings/keys), click **New SSH key** button.

![New SSH key page on GitHub](assets/github-add-ssh-key.png "Adding SSH key to GitHub")

Save the key and go back to terminal. Open file ~/.ssh/config using:

```shell
cd ~/.ssh
touch config
open config
```

And append following lines at the end of the file:

```text
Host github.com
  HostName github.com
  IdentityFile ~/.ssh/github
```

Save the file and close the editor.

After everything is set up, you can then check everything is working properly by executing command:

```shell
ssh git@github.com
```

If the key is set up properly, following message should be displayed:

```text
PTY allocation request failed on channel 0
Hi ihlavnicka! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

## Create GitHub repository
Go to [New repository](https://github.com/new) page on GitHub.

![Create repository on GitHub](assets/github-create-repository.png "Create repository on GitHub")

Select name, optionally description and choose whether the repository should be public (accessible to everyone) or private (accessible only to you and whoever you invite).

Then click **Create repository** button.

In your newly created repository, click the **<> Code** button and select **Local** tab and **SSH** option below

![Get git clone repository SSH](assets/github-clone-project.png "Clone repository SSH")

Copy the URL (will be used in next section)

## Create new project from remote repository

1. Start IntelliJ Idea
2. On the start page, click button **Get from VCS**
3. Select directory where the new project should be created
4. Paste the SSH path copied in previous step (should always start with `git@github.com`, if it starts with `https://`, it **won't** work!)
5. Click **Clone** button. If everything is set up correctly, the project should be cloned from remote repository, without asking for credentials.
6. If the IDE asks you whether you trust the project, select **trust**
7. Copy the **whole** content from previously generated project skeleton (do not forget hidden files! If you cannot see any hidden files between the extracted files, press <kbd>&#8984;</kbd>+<kbd>&#8679;</kbd>+<kbd>.</kbd> to show hidden files)

Now you should have the project set up.