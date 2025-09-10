### Pertinent links
This Gist supports a training video I developed on YouTube. You can access the video here:

**Watch the video**

<a href="http://www.youtube.com/watch?feature=player_embedded&v=zijOXpZzdvs" target="_blank">
 <img src="http://img.youtube.com/vi/zijOXpZzdvs/mqdefault.jpg" alt="Watch the video" width="560" height="315" />
</a>

This is a [Bit.ly](http://bit.ly/3L2WEdZ) link to the Gist

This is the [full link](https://gist.github.com/BillRaymond/db761d6b53dc4a237b095819d33c7332#file-dockerfile) to the Gist.

### Override GEM-based themes

[reference](https://jekyllrb.com/docs/themes/)

By default, Jekyll uses Gem-based themes. That means you cannot see the `_layouts`, `_includes`, and other folders.

You can override the theme and modify some or all of the files by copying them over to your Jekyll folder. Here are the steps:

1. Open the Jekyll folder in Visual Studio Code with the Docker container running
2. Type CONTROL+` to open a terminal window
3. Type `bundle info --path themename`, where "themename" is the name of your theme. By default, Jekyll uses Minima, so you would type:
    `bundle info --path minima`
    The result will look something like this:
    /usr/local/src/rbenv/versions/3.1.2/lib/ruby/gems/3.1.0/gems/minima-2.5.1
4. Using the example above, let's say we want to override the entire theme. First, make sure you are running a terminal window you are in the root folder of your working Jekyll site's repo. Copy the contents of the theme folder to your folder by typing:
    `cp /usr/local/src/rbenv/versions/3.1.2/lib/ruby/gems/3.1.0/gems/minima-2.5.1/. . -r -p`
    Now all the theme folders and files will appear

#### Optional steps
The following steps may or may not work for you, but
I include them as additional steps to fully remove
the dependency to the Minima theme.
5. Open the `_config.yml` file and comment out the theme entry. For example:
    If you use the Minima theme, you will see the entry `theme: minima`
    Change that entry to `# theme: minima` or delete it completely
6. Open your `Gemfile` and remove or comment out the theme. For example:
    If you use the Minima theme, you will see the entry: `gem "minima", "~> 2.0"`
    Change that entry to `# gem "minima", "~> 2.0"` or remove it completely
7. Save the files `_config.yml` and `Gemfile`
8. In the terminal window, type:
    ```
    bundle install
    bundle update
    ```
9. Git commit your changes and you can now modify any of the files you like


## Install the software prerequisites
1. Go to https://git-scm.com and download, install, and configure Git
2. Go to https://code.visualstudio.com and download and install the version of Visual Studio Code (VSC) for your operating system and chipset
3. Go to https://github.com and sign up for a free account. Make sure you can sign in completely before continuing
4. Go to https://docker.com and download and install Docker Desktop for your operating system and chipset. Also, sign up for a Docker account and make sure you sign in with that account in Docker desktop

## Configure desktop software
1. Go to https://git-scm, select the Pro Git book and follow the steps to install and configure Git
2. Run the Docker Desktop app and verify you are logged in
3. Run Visual Studio Code and install two extensions: Docker (from Microsoft) and Dev Containers (from Microsoft)
4. Also in Visual Studio Code, go to the Gear icon, select Settings, and then search for "Use Editor as Commit Input". De-select that option. This will help you follow along with how I use Visual Studio Code. This is an optional setting
5. Quit Visual Studio Code and then run it again so all the changes you made take effect
 
## Create a Repository (repo/folder) on your computer
1. Go to File->Open Folder and create a new folder. Call it "github-pages-with-docker"
2. Make note that you can learn more about Jekyll by going to the official Jekyll website at https://jekyllrb.com. You can select the `Docs` link and the `Installation` link to see installation requirements
3. You can find a Docker image to start with at https://hub.docker.com. In this video, I search for Ubuntu and then locate the "Docker Official Image" of Ubuntu
4. In VSC with the open folder, create a new file and call it `Dockerfile`
5. Type `FROM ubuntu:22.04` in the Dockerfile and press return and save the file
6. Type CMD or CTRL + P on your comptuer and type "Open folder in container" and press return
7. Open the folder you just created
8. When prompted, select the Dockerfile option
9. When prompted for other features, just select the Ok button
10. VSC will build images, containers, and volumes in Docker Desktop
11. VSC will display "Dev Container: Existing Dockerfile" at the bottom left of the app. Now you know you are running in Docker
12. Kill the terminal window (trash icon)

## Create the Ruby and Jekyll Docker container 
1. Go to the following link to open the GitHub gist files for this training: https://bit.ly/3L2WEdZ
Just in case the Bitly link does not work, here is the full link:
https://gist.github.com/BillRaymond/db761d6b53dc4a237b095819d33c7332#file-dockerfile
2. Locate the code that represents the Dockerfile, click the Raw button, and then select all the text and copy it
3. Open the Dockerfile you just created and remove all contents
4. Paste all the code into the Docker file you just copied from the Gist
5. Save and close the Dockerfile
6. Type CMD or CTRL + P on your keyboard, type "Rebuild container" and press return on your keyboard
7. The Docker image and container should rebuild

This Docker image will set up all the dependencies required for Ubuntu and Ruby. It will also install Jekyll, but it will not create the Jekyll website.

## Create the Jekyll website
At this point, you created a Dockerfile and defined the operating system and dependencies. The VSC Dev Containers app created a Docker image and a working container for you to run code.

1. Return back to the Gist: https://bit.ly/3L2WEdZ
2. Locate the shell file (.sh) that represents code you run after Docker, select the Raw button, select all the text, and then copy it to your clipboard
3. Return to VSC, and with the folder open that contains the Dockerfile, create a new file and name it "run-once.sh" (the filename does not matter, so long as you know what it is)
4. In the new shell file, paste the text you just copied from the Gist
5. Save the Shell file
6. Open the VSC terminal window by typing CTRL + `
7. Type `sh run-once.sh` and press return
8. The script will run through all the steps mentioned later in this section
9. The script will inform you as to what to do next. These steps may change over time, but following are the next steps
10. Open the newly create `_config.yml` file and modify the `baseurl` and `url` entries:
baseurl: "/github-pages-with-docker"
url: "https://YourUserName.github.com"
11. Go back to the terminal window and type:
bundle exec jekyll serve --livereload
12. Select the port 4000 link that displays (do not select "open browser" if you are prompted by VSC).
13. A browser window opens. Verify the site is running.
13. Back in VSC, close any open files and kill the terminal window
14. Type CMD or CTRL + P, type "commit all" and press return. Type "update config" and press return


This shell file will create a new Jekyll website, create a .gitignore file, inform the Jekyll site that it is specifically designed for GitHub Pages. The script will also add a technology Jekyll requires called webrick. Finally, the script will install all the components Jekyll requires and display a list of next steps.

You now have a Jekyll website that is running locally on your computer by way of running inside a Docker container.

## Publish, push, and configure GitHub Pages
When you push your code to GitHub, GitHub Pages will automatically update your website. However, you have to get that site up and running in GitHub first, so these are the steps you will follow to do that.

1. Type CMD or CTRL + P on your keyboard, type "Publish to GitHub" and press return on your keyboard
2. Select `Publish to GitHub public repository` and press return on your keyboard
3. Type CMD or CTROL + P on your keyboard, type "Git: Push" and press return on your keyboard
4. Go to https://github.com and sign in. Go to your list of Repositories and select the newly created "github-pages-with-docker" repo
5. Select the Settings option for your repo
6. Select the Pages item
7. In the Source section, select "Deploy from Branch"
8. In the Branch section, select "main" (or master or whatever is your default branch) and also select "/(root)
9. Select the Save button
10. Go back to your github-pages-with-docker repo
11. Locate the "About" section and select the cog (gear icon)
12. Select the "use your GitHub Pages website" and save changes
13. You will return to your repo and now you can select the website. Your browser will display your new website. Note that it might take a few minutes to update

In this section, you published your local repo to GitHub. You then pushed your local code into that newly create GitHub repo. You enabled GitHub Pages for the first time, and then you added a link to the website for easy access later. Finally, you verified that GitHub Pages is running successfully.

## Modify your GitHub Pages site
In this section, you will learn a workflow to make changes locally on your Docker container and then update GitHub.

1. If you are not already running VSC, type CMD or CTRL + P on your keyboard and open the git-hub-pages-with-docker folder
2. Type CMD or CTRL + ` on your keyboard to open a terminal window and type:
bundle exec jekyll serve --livereload
3. While holding down the CMD or CTRL key on your keyboard, select the URL running on port 4000. A browser window should open
3. Back in VSC, open the `index.md` file and under the last set of "---" items, add a new line and type "Hello World!"
4. Save the index.md file
5. Go back to your browser running port 4000 and the words "Hello World!" should appear on the home page
6. Type CMD or CTRL + P on your keyboard, type "Git: Commit All" and then press return on your keyboard
7. Type "added hellow world! to index" and press return on your keyboard
8. Type CMD or CTRL + P on your keyboard, type "Git: Push" and then press return on your keyboard
9. In your browser, go to the live website, which will look something like the following link:
https://YourGitHubUserName.github.com/github-pages-with-docker
10. Continue to refresh your browser window until you see "Hello World!"

In this section you learned a basic workflow to make changes on your comptuer, test them, then commit them locally. When ready, you push those changes up to your GitHub repo and you will see the changes.

## Override a Gem-based theme
When you create a new Jekyll site without the "--blank" switch, it will create a Jekyll website that uses the default Jekyll theme named minima. Minima and most other Jekyll themes are Gem-based themes. You cannot see theme files by default. In this section, you will learn how to override the theme by copying the theme files to your repo

1. Run VSC with the Dev Container open
2. Type CTRL + ` on your keyboard to open the terminal
3. Type:
bundle info --path minima
4. You will see a folder that displays the currently installed version of minima. Select and copy that text. It will look something like this (I will use this as the example, but oyu use the text you copied):
/usr/local/src/rbenv/versions/3.1.2/lib/ruby/gems/3.1.0/gems/minima-2.5.1
5. In the terminal window, type:
cp /usr/local/src/rbenv/versions/3.1.2/lib/ruby/gems/3.1.0/gems/minima-2.5.1/. . -p -r
6. Verify new folders and files are created, like:
_includes
_layouts
_sass
etc
7. In the terminal window, type:
bundle exec jekyll serve --livereload
8. CMD or CTRL + click the running port 4000. The browser will open with your running website
9. Back in VSC, select the Search icon and then search for "post-title". Locate and open the SASS file that displays in the search results. 
10. Locate the ".post-title { }" area and within the brackets, add the following lines (there will already be other lines of code in there):
background-color: black;
color: yellow;
11. Save the file and then go to the browser running your local website. Select the "Welcome to Jekyll!" link and you will find the title displays in yellow text with a black background
12. Go to VSC, type CMD or CTRL + P, type "Git: Commit all" and press return on your keyboard. Type "override minima theme", and then press return on your keyboard
13. Type CMD or CTRL + P on your keyboard, type "Git: Push", and then press return on your keyboard.
14. Open a browser and go to GitHub Pages. Verify all the new files are in the repo. You can also go to your live GitHub Pages website to verify the changes you made take effect

Most themes are Gem-based, which means you will not see the code in your repo. If a developer changes their theme and you type "bundle install", the theme will automatically update. You may not want that. If you want to modify the theme in any way, it is a good idea to completely override it by copying the files installed elsewhere in your Docker container and putting them into your repo.

## Start your site on a new computer
Let's say you bought a new computer. You did not backup anything. Now you need to completely rebuild your site. In the accompanying video for this training, I delete all containers, images, and volumes in Docker. I even delete the folder.

1. Run VSC and type CMD or CTRL + P and type "Git: Clone". Select "Clone from GitHub", and then select "github-pages-with-docker". Open the folder.
2. If you are prompted, select the "Open in container" dialog or type CMD or CTRL + P and type "Open folder in container" and press return on your keyboard. Select the same github-pages-with-docker folder
3. Your Docker image and container will open
4. Type CTRL + ` on your keyboard to run the terminal window and then type the following commands, one at a time:
bundle install
bundle upate
bundle exec jekyll server --livereload
5. CTRL + click the server running on port 4000. Your browser should open and display your Jekyll site

So long as you regularly push your code back up to GitHub, your website is never lost! All you need to do is update the Ruby Gem files with the `bundle install` and `bundle update` commands

## Clone a GitHub Pages repo that does not use Docker
Let's say you see a GitHub Pages repo that has a great website you want to start from. However, the repo may not use Docker, so let's use our own.

1. Go to GitHub.com and search for "Hipster Bill Raymond". Select the Users link and then select HipsterBillRaymond
2. Locate the my-rockin-github-pages repo and select it
3. Select the "Fork" option
4. Leave the repo as the same name and only copy the main (or master, etc) branch
5. Now your forked copy of the repo displays. Select the cog (gear) next to the "About" section and modify the url to use your username, so the link looks something like this:
https://YourGitHubUserName.github.io/my-rockin-github-pages
6. Save changes and then select the Settings option for the repo
7. Select the Pages item
8. Just as before make these changes:
Source: Deploy from branch
Branch: main
Branch: /(root)
Select the Save button
9. Go back to the repo, wait for the site to be built, and then select the link in the About section to verify it is running
10. Go back to the repo, select the Code item, and then select the _config.yml and select the Edit item
11. Locate the url and change the setting to something like this:
https://MyGitHubUsername.github.io
12. Select the Save/Commit option and follow the steps to save your changes
13. Run VSC, type CMD or CTRL + P, type "Clone from GitHub" and press return on your keyboard. Select the repo named my-rockin-github-pages and press return on your keyboard
14. Go to the Gist at https://bit.ly/3L2WEdZ and locate the Dockerfile. Select the Raw button, then select all the text and copy it to the clipboard
15. Go to VSC and create a new file. Type "Dockerfile"
16. In the newly created Dockerfile, paste the text you just copied from the Gist and save the Dockerfile
17. Type CMD or CTRL + P, type "Commit all", and type "add Dockerfile" and press return
18. Type CMD or CTROL + P, type "Open folder in container" and press return
19. A dialog appears. Select my-rockin-github-pages and then select the Open button
20. Type CTRL + ` on your keyboard, and then type the following commands one at a time:
bundle install
bundle update
bundle exec jekyll serve --livereload
21. CTRL + select the server running at port 4000. The browser should open and you will see the new site running
22. Go back to VSC, open the index.md file and locate the "Welcome to my rockin site!!" text and change it to something like:
"Welcome to Bill Raymond's rockin site!!"
23. Save the index.md file
24. Type CMD or CTRL + P on your keyboard, type "commit all", type "update site", and then press return on your keyboard
25. Type CMD or CTRL + P on your keyboard, type "git: push", and press return on your keyboard
26. Go back to GitHub and wait for the commit to complete, then select the URL in the about section. Verify the site is still running

You now have the basics down!


TOC
00:00 Introduction to GitHub Pages and Docker
04:22 Prerequisites
05:20 Configure desktop apps
08:08 Create a repo and test Docker
17:19 Create the Ruby and Jekyll Docker container
23:51 Create the Jekyll website
32:48 Publish, push, and configure GitHub Pages
36:05 Modify your GitHub Pages site
40:38 Override a Gem-based theme
47:58 Start your site on a new computer
52:38 Clone a GitHub Pages repo that does not use Docker
