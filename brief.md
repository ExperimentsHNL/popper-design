# Popper Brief # 

## Table of Contents ##

-	[Introduction](#Introduction)
	
-	[The Plumbing](#ThePlumbing)

-	[Unity Programmer Brief](UnityProgrammerBrief)

-	[Web Developer Brief](WebDeveloperBrief)

-	[Web Designer Brief](WebDesignerBrief)	 

## <a name="Introduction" id="anchor4">Introduction</a> ##

**Popper** is a platform that allows social science researchers to create and 
run **online experiments** to test human behavior. It consists of three pieces: 

1. **The Popper Software Development Kit**, which the reseacher uses to create the 
experiments and visualize them as online games on par with Facebook and App Store 
games; 

2. **The Popper Dock**, which is a website that the researcher uses to launch her 
experiments online and watch them in real time;  

3. **The Game Website**, where subjects participate in experiments by 
playing games. 

### Social scientists would like to know *when* and *why* people... ###

...cooperate

...cheat

...respond to rewards

...respond to punishment

...and do what they do.

### Testing human behavior is hard... ###

...but not because of a lack of data. After all, humans make tens of thousands
of decisions every day. Social scientists only have to capture a few of these
decisions in a controlled setting. This data is hard to collect because of two main reasons: 
money and time. 

Let's take a look at an example. Say Rina the Economist wants to study when 
people cooperate by testing the classical game theory scenario,
[Prisoner's Dilemma](http://en.wikipedia.org/wiki/Prisoner's_dilemma). 

First, Rina must learn how to program and work with 
[outdated software](http://www.iew.uzh.ch/ztree/index.php) from the 1990s
to design her experiment. Her subjects will have to fill in boxes with 
numbers--a task so boring that Rina will have to pay them each $15 to $20 
per hour.

Next, she must find a multi-million dollar social science experiments laboratory 
and then several weeks securing enough subjects to run her trial. This process 
often takes several weeks. Some of her subjects might not show up, and Rina 
might have to recruit subjects a second or third time until enough people have 
participated. More weeks pass.

By the time this process is over, 1 month has passed and Rina has spent
thousands of dollars. And that's just for Trial 1.

### Popper solves both problems. ###

What if a trial could take 1 day instead of several months? What if each trial
cost a few hundred dollars rather than several thousand?

Along comes Popper to the rescue!

Using the Popper SDK, Rina creates an experiment using [uScript](http://forum.unity3d.com/threads/84594-Introducing-the-uScript-Visual-Scripting-Tool-for-Unity!), 
an intuitive visual scripting tool. She does not need to know a single line of 
code--only how to drag and drop boxes. uScript works within 
[Unity](http://unity3d.com/), the most commonly used game engine in the world.
With these tools, Rina can create an online game on par with the best Facebook 
and App Store games without knowing a single line of code--all she has to do 
is drag and drop boxes to tell Unity what is supposed to happen in each 
game. She frames her experiment using Unity's palette of professionally 
developed options--a card game, shooter, or simple RPG. With a few clicks, Rina
can create an online shooter that is actually a social science experiment 
in disguise. 

Rina launches the game from the online Popper dock onto the Game Website. Rina 
finds people to play her game on the internet using [Amazon Mechanical Turk](https://www.mturk.com/mturk/welcome) 
or [oDesk](https://www.odesk.com/?_redirected). Subjects sign up within minutes. 
They play the games not just for pay, but because they're fun. Subject payment
costs are much lower online. Rina can now run 10 trials per day instead of per 
year. She can monitor her experiments in real time from the Popper Dock. Total 
cost of a trial? 1 day and a few hundred dollars, rather than 1 month and several 
thousand dollars. Rina gets tenure at a top university based on her work in 
experimental economics and then wins the Nobel Prize.

## <a name="ThePlumbing" id="anchor5">The Plumbing ##

Popper consts of several different pieces. Below is a diagram showing the 
architecture of Popper. Click <a href="https://github.com/Experiments/popper-design/blob/master/popper_overview.png?raw=true" target="_blank">here</a> for a larger view.

<a href="https://github.com/Experiments/popper-design/blob/master/popper_overview.png?raw=true" target="_blank">![Popper Overview](https://github.com/Experiments/popper-design/blob/master/popper_overview.png?raw=true)</a>

1. Researcher downloads the Popper SDK from Github using their desktop Github client. 

2. Researcher opens the Popper SDK in Unity and creates an experiment consisting of the Client and Master Client. The Client is the visual front end of the experiment. It is ultimately executed on a player's computer or phone. The Master Client is the underlying logic of the experiment and ultimately runs in the Experiment Server.

3. Researcher uploads the experiment, which consists of the Master Client, Client, and Source Code, to his local GitHub repository. 

4. GitHub Client syncs the contents of the local repository with the remote online GitHub repository. 

5. Researcher logs into the online Researcher Dashboard and selects an experiment to launch a trial. 

6. The Popper Web Service downloads the Master Client that corresponds to the selected experiment.

7. The Popper Web Service uploads this Master Client to the Experiment Server.

8. The Popper Web Service remotely starts the Master Client on the Experiment Server and connects it to the Photon Server, creating a trial. 

9. The Popper Web Service announces the trial to eligible players in the Popper Subject Pool.

10. Interested players log into the Player Site. 

11. The Player Site downloads the Client from the experiments repository on GitHub.

12. The Player Site opens the Client on each player's browser or phone. The player sees the game.

13. Each player's Client connects to the current trial running on the Photon Server.

14. The Popper Web Service establishes a connection with Photon Server via Photon Client. The trial begins.

15. The Researcher Site monitors the ongoing trial via Photon Client.

16. All events in the trial are recorded in the Popper database.

17. Researcher monitors the ongoing trial in his browser. Once the trial ends, Researcher reviews and approves subject payments.

18. The Popper Web Service posts payments to players' accounts. 

### Role 1: Unity Programmer ###

The Unity Programmer works with us to build on top of existing Popper code. 
This work involves the Unity, uScript, and Photon Server components of the Popper 
SDK. 

Go to the [Unity Programmer Brief](#UnityProgrammerBrief). 

### Role 2: Web Developer ###

The Web Developer works with us to integrate the experiments deployed on 
GitHub with the Ruby server. Popper consists of two websites: 1. Popper Dock, 
which is where the researcher launches and monitors experiments, and 2. the 
Game Website, where subjects play online games. 

Go to the [Web Developer Brief](#WebDeveloperBrief). 

### Role 3: Web Designer ###

The Web Designer works with us to design the UI/UX of the two website components 
of Popper: Popper Dock (for researchers) and the Game Website. The designer 
also works with us on the branding and logo of Popper.

Go to the [Web Designer Brief](#WebDesignerBrief). 

## <a name="UnityProgrammerBrief" id="anchor1">Unity Programmer Brief</a> ##

In progress.

<!-- In this section, we'll explain the user workflow related to Unity, tech specs, 
and other good stuff. 

### Big-Picture Overview ###

![Temporary Plumbing Image](http://static4.depositphotos.com/1009645/357/v/450/dep_3577496-Architectural-blueprint-background.-Vector.jpg)

There are five discrete tasks that remain to be done for the MVP:

1. Refactor existing code; 

2. Standardize the structure of 6 stock games; 

3. Develop uScript node packages; 

4. Simplify the uScript workflow; 

5. Raw logging functionality on Photon.

The remainder of this brief will run through a detailed workflow of the Unity, 
uScript, and Photon Server portions of Popper. 

### Step 1: Foo ###

![Temporary Plumbing Image](http://static4.depositphotos.com/1009645/357/v/450/dep_3577496-Architectural-blueprint-background.-Vector.jpg)

Do this, this, then that. 

### Step 2: Foo ###

![Temporary Plumbing Image](http://static4.depositphotos.com/1009645/357/v/450/dep_3577496-Architectural-blueprint-background.-Vector.jpg)

Do this, this, then that. 

### Step 3: Foo ###

![Temporary Plumbing Image](http://static4.depositphotos.com/1009645/357/v/450/dep_3577496-Architectural-blueprint-background.-Vector.jpg)

Do this, this, then that. 

### <font color="red">Caution!</font> ###

1. Be care of this.

2. Also this.

3. Also that. 
 -->
## <a name="WebDeveloperBrief" id="anchor2">Web Developer Brief</a> ##

In this section, we'll explain the user workflow related to the Web portion of Popper, tech specs, 
and other good stuff. 

### Big-Picture Overview 

The two website components of Popper are separate. The purpose of Popper Dock 
is to allow researchers to create, run, and monitor experiments, as well as 
share experiments with other social science researchers. The Game Website 
is for players only. Its purpose is to be engaging enough that players would 
want to play games on the site for the sake of the games themselves, not just 
for pay.  

### Researcher Website 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_base.png?raw=true)

#### 1. Landing Page 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_landing.png?raw=true)

The purpose of the landing page is to introduce the researcher to Popper and allow her to sign up. 
The researcher should first see an introduction video (which we will create). Afterwards, she 
should be able to browse the Experiment Library (Page 4). She should also be able to see the 
logos/shields of the universities of other researchers who use Popper. 

A navigation bar should allow the researcher to go to go to the Sign Up, About, Documentation, 
and Experiment Library of Popper. The link to Documentation will bring the researcher to a 
GitHub repository, and will not be an internal page on the Researcher Website. This navigation 
bar should be consistent and available throughout the entire website. 

#### 2. Signup 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_signup.png?raw=true)

The Signup page allows the researcher to create a Popper account and go through the steps 
necessary to begin running experiments online. It should include fields for the researcher 
to provide her demographic information as well as research-specific information such as 
her field, institution, and the name of her laboratory. Once the researcher has filled in this 
basic information, she will be taken to a page (still part of "Signup"), but on a separate page 
that provides her with step-by-step instructions for downloading the Popper SDK and creating/linking 
a GitHub account.

Downloading the Popper SDK will be done on our website, as we will be redistributing Unity with 
their permission. Creating a GitHub account will be done on the GitHub website. Linking the 
researcher's GitHub account with our GitHub server will be done with the click of one button 
on our page, which takes the researcher to an external GitHub page that authenticates the 
connection of their account. 

#### 3. Researcher Dashboard 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_dashboard.png?raw=true)

Once the researcher has completed signup, she will be taken to the Researcher Dashboard. Here, 
the researcher has an overview of all her trials and experiments that she is following. She 
should see two main elements in her Dashboard: an Experiments Feed and a Trials Feed.  

The Experiments Feed conceptually resembles the feed visible within a GitHub account. The 
researcher can see commits and changes to existing experiments that other researchers have made. 
To clarify, an **experiment** is a particular set of game logic framed as an online game, and its 
purpose is to test human behavior. Experiments consist of multiple **trials.** Researchers may 
choose to run trials using experiments that other researchers have already designed and made 
publicly available. The idea is for researchers to be able to share experiments with each other.

The second element of the Dashboard is the list of the researcher's own trials. This Trial Feed 
will be dynamic, like the Experiments feed. The researcher will see important new information about 
each of her ongoing trials. She should see the name, status, time stamp, underlying experiment, 
payment information, and number of subjects associated with each trial, as well as any changes 
to any of these pieces of information. The status of the trial is one of 5: Error, Awaiting Launch 
(the researcher has not yet launched the trial), Ongoing, Payment Pending, and Completed.  

#### 4. Experiment Library 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_library.png?raw=true)

The Experiment Library includes a list of all available experiments. We plan to launch with six 
stock experiments, each of which can be run with a different frame. The experiments should each 
be accompanied by an appropriate image, which we will provide. 

Two audiences are served by the Experiment Library. 1. Researchers without an account can browse 
the Library, but cannot initiate a trial. If they attempt to do so, they should be prompted to 
create an account. 2. Researchers with an account can use the Experiments Library to select 
an experiment within which to launch a trial.

Basic information should accompany each of the images of experiments available in the Library: 
a brief description, available game frames, date created, number of subjects, and number of 
trials run. A clear link or button next to the experiment should allow the researcher to 
"Create Trial".

#### 5. Create Trial 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_trial.png?raw=true)

Once the researcher selects an experiment, she can specify the parameters of the trial that 
she would like to launch to run this experiment. Again, researchers without an account cannot 
access this page and will be redirected to the Signup page instead. 

The researcher should be able to specify her subject pool, the start and end date of the trial, 
payment amounts for subjects, the frame of the experiment (in other words, the type of game that 
her subjects actually see), and select details relating to the frame of the experiment. 

#### 6. About 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_about.png?raw=true)

Just a stock about page using the same template as the Landing Page.

#### 7. Researcher Profile 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_profile.png?raw=true)

The Researcher Profile consists of the information that the researcher provided during the signup 
process as well as privacy settings.

#### 8. Monitor Trials 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_monitor.png?raw=true)

The researcher can find out more information about a trial displayed in the Trial Feed in the 
Researcher Dashboard by clicking on the trial. This takes her to the Monitor Trials page, which 
includes more specific information about the selected trial. 

What the researcher sees depends on the current status of the trial. If it is Awaiting Launch, 
the researcher will be taken instead to the Create Trial page. If it is Ongoing, she will be 
able to see the profiles of players who are participating in her game as well as realtime 
results. If the trial displays Payment Pending in the Researcher Dashboard, the researcher 
will see payment authorization fields that are linked to whichever labor market that provided 
her subjects--for the time being, either Amazon Mechanical Turk or oDesk. If the trial is 
Completed, the researcher can see the profiles of players and download the results log from 
the trial. 

#### <font color="red">Caution!</font> 

1. Be careful of this.

2. Also this.

3. Also that. 

### Player Website 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_base.png?raw=true)

#### 1. Signup 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_signup.png?raw=true)

Players will not be able to see available games (trials) unless they are signed in. We would like
to know precisely who is reviewing available trials. For this reason, the signup page is the 
landing page of the Player Website. Barriers to entry for the player should be minimal, especially 
since the player is most likely already arriving from an external site (Amazon Mechanical Turk 
or oDesk). The player should thus be able to create an account using an existing Facebook or 
Twitter account. The signup page should also be miminalistic in terms of data gathered from the 
player, asking only for a username, password, and the player's age. More in-depth demographic
information will be gathered later, once the player has created an account--perhaps on a separate 
page, using the same template. This information will be used to determine which trials are visible 
to the player in the Lobby (2). 

Players who already have an account will use this page to log in. 

#### 2. Lobby 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_lobby.png?raw=true)

Players who are visiting the site directly without having pre-selected a game to play will be 
take to the lobby to browse games (ongoing trials). The graphics and UI/UX should compel the 
player to want to stay on the website to play a lot of games. We envision perhaps a screenshot 
of each game to accompany a link to each of the games. Basic information also accompanies 
each game visible to the player in the lobby: pay, trial end date, number of current players, 
and a description of the game itself. Only games that match the player's demographics will 
be visible.

#### 3. Game 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_game.png?raw=true)

The player plays the game on this page. 

#### 4. About 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_about.png?raw=true)

Basic About page, perhaps reusing the same template as the Signup page. 

#### 5. Player Profile 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_profile.png?raw=true)

The player can view his history of games on the profile page, as well as manage his account 
information and privacy settings. 

#### <font color="red">Caution!</font>

1. Be careful of this.

2. Also this.

3. Also that. 

## <a name="WebDesignerBrief" id="anchor3">Web Designer Brief</a> ##

In this section, we'll explain the user workflow related to the Web design portion of Popper, tech specs, 
and other good stuff. 

### Big-Picture Overview 

The two website components of Popper are separate. The purpose of Popper Dock 
is to allow researchers to create, run, and monitor experiments, as well as 
share experiments with other social science researchers. The Game Website 
is for players only. Its purpose is to be engaging enough that players would 
want to play games on the site for the sake of the games themselves, not just 
for pay. 

Accordingly, the feel of the two websites should be very different. We are 
seeking a classical and academic yet modern tone for the Popper Dock. The 
sole purpose of the Game Website is to attract as many players as 
possible and keep them on the site playing games for as long as possible. 
There will be no links connecting Popper Dock to the Game Website, so no 
thematic or design similarities between the two sites are necessary. 

### Researcher Website 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_base.png?raw=true)

#### 1. Landing Page 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_landing.png?raw=true)

The purpose of the landing page is to introduce the researcher to Popper and allow her to sign up. 
The researcher should first see an introduction video (which we will create). Afterwards, she 
should be able to browse the Experiment Library (Page 4). She should also be able to see the 
logos/shields of the universities of other researchers who use Popper. 

A navigation bar should allow the researcher to go to go to the Sign Up, About, Documentation, 
and Experiment Library of Popper. The link to Documentation will bring the researcher to a 
GitHub repository, and will not be an internal page on the Researcher Website. This navigation 
bar should be consistent and available throughout the entire website. 

#### 2. Signup 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_signup.png?raw=true)

The Signup page allows the researcher to create a Popper account and go through the steps 
necessary to begin running experiments online. It should include fields for the researcher 
to provide her demographic information as well as research-specific information such as 
her field, institution, and the name of her laboratory. Once the researcher has filled in this 
basic information, she will be taken to a page (still part of "Signup"), but on a separate page 
that provides her with step-by-step instructions for downloading the Popper SDK and creating/linking 
a GitHub account.

Downloading the Popper SDK will be done on our website, as we will be redistributing Unity with 
their permission. Creating a GitHub account will be done on the GitHub website. Linking the 
researcher's GitHub account with our GitHub server will be done with the click of one button 
on our page, which takes the researcher to an external GitHub page that authenticates the 
connection of their account. 

#### 3. Researcher Dashboard 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_dashboard.png?raw=true)

Once the researcher has completed signup, she will be taken to the Researcher Dashboard. Here, 
the researcher has an overview of all her trials and experiments that she is following. She 
should see two main elements in her Dashboard: an Experiments Feed and a Trials Feed.  

The Experiments Feed conceptually resembles the feed visible within a GitHub account. The 
researcher can see commits and changes to existing experiments that other researchers have made. 
To clarify, an **experiment** is a particular set of game logic framed as an online game, and its 
purpose is to test human behavior. Experiments consist of multiple **trials.** Researchers may 
choose to run trials using experiments that other researchers have already designed and made 
publicly available. The idea is for researchers to be able to share experiments with each other.

The second element of the Dashboard is the list of the researcher's own trials. This Trial Feed 
will be dynamic, like the Experiments feed. The researcher will see important new information about 
each of her ongoing trials. She should see the name, status, time stamp, underlying experiment, 
payment information, and number of subjects associated with each trial, as well as any changes 
to any of these pieces of information. The status of the trial is one of 5: Error, Awaiting Launch 
(the researcher has not yet launched the trial), Ongoing, Payment Pending, and Completed.  

#### 4. Experiment Library 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_library.png?raw=true)

The Experiment Library includes a list of all available experiments. We plan to launch with six 
stock experiments, each of which can be run with a different frame. The experiments should each 
be accompanied by an appropriate image, which we will provide. 

Two audiences are served by the Experiment Library. 1. Researchers without an account can browse 
the Library, but cannot initiate a trial. If they attempt to do so, they should be prompted to 
create an account. 2. Researchers with an account can use the Experiments Library to select 
an experiment within which to launch a trial.

Basic information should accompany each of the images of experiments available in the Library: 
a brief description, available game frames, date created, number of subjects, and number of 
trials run. A clear link or button next to the experiment should allow the researcher to 
"Create Trial".

#### 5. Create Trial 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_trial.png?raw=true)

Once the researcher selects an experiment, she can specify the parameters of the trial that 
she would like to launch to run this experiment. Again, researchers without an account cannot 
access this page and will be redirected to the Signup page instead. 

The researcher should be able to specify her subject pool, the start and end date of the trial, 
payment amounts for subjects, the frame of the experiment (in other words, the type of game that 
her subjects actually see), and select details relating to the frame of the experiment. 

#### 6. About 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_about.png?raw=true)

Just a stock about page using the same template as the Landing Page.

#### 7. Researcher Profile 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_profile.png?raw=true)

The Researcher Profile consists of the information that the researcher provided during the signup 
process as well as privacy settings.

#### 8. Monitor Trials 

![Image](https://github.com/Experiments/popper-design/blob/master/rworkflow_monitor.png?raw=true)

The researcher can find out more information about a trial displayed in the Trial Feed in the 
Researcher Dashboard by clicking on the trial. This takes her to the Monitor Trials page, which 
includes more specific information about the selected trial. 

What the researcher sees depends on the current status of the trial. If it is Awaiting Launch, 
the researcher will be taken instead to the Create Trial page. If it is Ongoing, she will be 
able to see the profiles of players who are participating in her game as well as realtime 
results. If the trial displays Payment Pending in the Researcher Dashboard, the researcher 
will see payment authorization fields that are linked to whichever labor market that provided 
her subjects--for the time being, either Amazon Mechanical Turk or oDesk. If the trial is 
Completed, the researcher can see the profiles of players and download the results log from 
the trial. 
 
#### <font color="red">Caution!</font> 

1. It is important that the significance of the name "Popper" is appropriately 
conveyed. Popper is named after [Karl Popper](http://en.wikipedia.org/wiki/Karl_Popper), 
the late philosopher of science who established the modern practice of 
hypothesis testing and much of scientific thought as we know it. "Popper" 
should not be confused with the action of "popping" or drugs.

2. Popper is a platform for the social sciences, not the natural sciences. All 
images and logos should avoid any allusions to the natural sciences, including 
test tubes, atoms, or microscopes. 

3. The Popper logo should work with both a black and light background, since 
Popper will need to be juxtaposed with the Unity platform, which has a black 
background.  

### Player Website 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_base.png?raw=true)

#### 1. Signup 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_signup.png?raw=true)

Players will not be able to see available games (trials) unless they are signed in. We would like
to know precisely who is reviewing available trials. For this reason, the signup page is the 
landing page of the Player Website. Barriers to entry for the player should be minimal, especially 
since the player is most likely already arriving from an external site (Amazon Mechanical Turk 
or oDesk). The player should thus be able to create an account using an existing Facebook or 
Twitter account. The signup page should also be miminalistic in terms of data gathered from the 
player, asking only for a username, password, and the player's age. More in-depth demographic
information will be gathered later, once the player has created an account--perhaps on a separate 
page, using the same template. This information will be used to determine which trials are visible 
to the player in the Lobby (2). 

Players who already have an account will use this page to log in. 

#### 2. Lobby 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_lobby.png?raw=true)

Players who are visiting the site directly without having pre-selected a game to play will be 
take to the lobby to browse games (ongoing trials). The graphics and UI/UX should compel the 
player to want to stay on the website to play a lot of games. We envision perhaps a screenshot 
of each game to accompany a link to each of the games. Basic information also accompanies 
each game visible to the player in the lobby: pay, trial end date, number of current players, 
and a description of the game itself. Only games that match the player's demographics will 
be visible.

#### 3. Game 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_game.png?raw=true)

The player plays the game on this page. 

#### 4. About 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_about.png?raw=true)

Basic About page, perhaps reusing the same template as the Signup page. 

#### 5. Player Profile 

![Image](https://github.com/Experiments/popper-design/blob/master/pworkflow_profile.png?raw=true)

The player can view his history of games on the profile page, as well as manage his account 
information and privacy settings. 

#### <font color="red">Caution!</font> 

1. Be careful of this.

2. Also this.

3. Also that. 