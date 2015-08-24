---
layout: post
title: How to Contribute to a GitHub Project
---

Want to contribute to a GitHub project but not sure how to get your code into the main repo? Here are the steps to take to start contributing to an open source GitHub project that is not your own.

**1.** When you are on the project's GitHub page click the fork button in the top right:

![_config.yml]({{ site.baseurl }}/images/Github/1.png)

After you click fork, the repo in its current state should be copied over to your repo list as one of your repos. Notice how in the screenshot below, the repo is now a repo of your username, and it says "forked from AFNetworking/AFNetworking" indicating we are no longer on the main repo page.

![_config.yml]({{ site.baseurl }}/images/Github/2.png)

**2.** Clone the forked repo you just made (rajohns/AFNetworking in this example). Copy the clone URL as shown below and do a **`git clone https://github.com/rajohns08/AFNetworking.git`**

![_config.yml]({{ site.baseurl }}/images/Github/3.png)

**3.** Assuming you have the GitHub desktop client downloaded, add the repo you just cloned.

![_config.yml]({{ site.baseurl }}/images/Github/4.png)

**4.** Make whatever changes you want to make to the codebase then commit then sync your changes to GitHub.

![_config.yml]({{ site.baseurl }}/images/Github/5.png)

**5.** Navigate back to the main repo page on GitHub and click the pull request button.

![_config.yml]({{ site.baseurl }}/images/Github/6.png)

**6.** Click "compare across forks" so you can choose to merge from your fork.

![_config.yml]({{ site.baseurl }}/images/Github/7.png)

**7.** Select your cloned repo from the head fork section.

![_config.yml]({{ site.baseurl }}/images/Github/8.png)

**8.** Click Create pull request.

![_config.yml]({{ site.baseurl }}/images/Github/9.png)

You will be presented with one more screen where you can add more details to your pull request if you would like. And that should be it! You will now have to wait on your changes to be merged in by the repo admin or someone with write access to the repo.
