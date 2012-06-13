# Popper Brief 

## Table of Contents

-	[Introduction](#Introduction)
	
-	[Overview of Popper Platform](#PopperOverview)

-   [Development Team](#DevelopmentTeam)

-	[Unity Programmer Brief](UnityProgrammerBrief)

-	[Web Developer Brief](WebDeveloperBrief)

-	[Web Designer Brief](WebDesignerBrief)	 

## <a name="Introduction" id="anchor4">Introduction</a> ##

**Popper** is a behavioral experiments platform that empowers researchers in economics, psychology, sociology, and political science to create an conduct complex large-scale online experiments. 


### Role of experiments

 Social scientists are interested in studying human behavior, and developing theories explaining it. Controlled experiments represent the main tool by means of which researchers are able to test the validity of proposed theories. All candidate theories must produce specific predictions (hypotheses) that can in principle be proven wrong. By subjecting such predictions to experimental test researchers falsify incorrect theories.

### Classical experiments

Conducting controlled experiments in social sciences is difficult. Unlike natural scientists who conduct their experiments with inanimate objects, social scientists experiment with live human beings. Human subjects cannot be forced to participate in experiments, and can also quit an ongoing experimental trial at any point. Participation thus has to be incentivized by monetary compensation that rewards completion of the trial. These trials are typically run in physical laboratories where invited volunteer subjects engange in simple decision tasks for $15-25/hour, and sometimes more depending on their performance. 

This approach has three serious limitations: 

1. It is very costly as it requires an equipped brick and mortar laboratory, and significant subject payments that typically exceed $500-1000 per trial. 

2. It is time-consuming, and requires recruiting local human subjects more than a week in advance of the trial. 

3. Local subject pools are relatively small, so large-scale trials require using laboratories in multiple geographical locations.

Apart from that, the software used in physical labs to create and conduct experiments is very outdated. The most popular package, [z-Tree](http://www.iew.uzh.ch/ztree/index.php), was created in the University of Zurich in the late 1990s and hasn't been updated since then.

### Online experiments

In the last 2-3 years researchers have started conducting experiments online, using subjects from various online labor markets, most notable [Amazon Mechanical Turk](http://mturk.com). This move has radically expanded the size of the available subject pool, and decreased subject payments, asexperimental subjects are no longer required to come to a physical lab, and can participate in trials from the comfort of their home.

However, move to online trials imposes several additional constraints on experimental design:

1. Lack of software. Most online trials have so far been limited to survey-style tasks that do not involve realtime interaction between subjects. And the researchers that did conduct multiplayer studies had to write the ad hoc software necessary to support such studies from scratch. No reusable framework capable of supporting multiplayer online trials is currently available on the market.

2. Low comprehension rates of written instructions. Online subjects frequently skim, or even ignore written experimental instructions.

3. High subject attrition rates. Even though in a physical lab subjects are allowed to quite the trial at any moment, doing so involves what is usually an uncomfortable interaction with the experimenter, while online subjects can quit a trial by simply closing a browser tab. This leads to very high attrition rates in trials where subjects get bored.

4. Lower degree of control over the experimental conditions. Subjects can potentially communicate with each other, collude, and cheat in other ways which undermines the internal validity of the experiment.

### Popper

Popper's goal is to address the above four problems. It will streamline the process of creating complex and visually compelling multiplayer experiments using professional game developing tools which include visual scripting and extensive library of template game assets. Popper will also provide researchers with extensive monitoring capabilites of remote subjects to minimize the possibility on cheating and other runtime irregularities.


## <a name="PopperOverview" id="anchor5">Overview of Popper Platform

Popper platform consists of four pieces: 

1. **Popper SDK** -- a set of tools based on Unity 3D game engine that the reseacher uses on their local computer to design experiments in the form of short multiplayer games;

2. **Experiments Library** -- GitHub-based online repository used for storing and sharing source code, as well as binary files of developed experiments;

3. **Researcher Site** -- a website that the researcher uses to launch and monitor online trials based on the experiments available in the **Experiments Library**;

4. **Player Site** -- a website that players (experimental subjects) use to browse and participate in trials launched by the researchers.


Below is a diagram showing the general architecture of Popper. Click <a href="https://github.com/Experiments/popper-design/blob/master/popper_overview.png?raw=true" target="_blank">here</a> for a larger view.

<a href="https://github.com/Experiments/popper-design/blob/master/popper_overview.png?raw=true" target="_blank">![Popper Overview](https://github.com/Experiments/popper-design/blob/master/popper_overview.png?raw=true)</a>

Typical workflow:

1. <font color="5185E8">Researcher</font> downloads the <font color="5C878F">Popper SDK</font> from <font color="5C878F">Github</font> using his desktop <font color="5C878F">Github</font> client. 

2. <font color="5185E8">Researcher</font> opens the <font color="5C878F">Popper SDK</font> in <font color="5C878F">Unity</font> and creates an experiment consisting of the <font color="5C878F">Client</font> and <font color="5C878F">Master Client</font>. The <font color="5C878F">Client</font> is the visual front end of the experiment. It is ultimately executed on a <font color="DB563B">player's</font> computer or phone. The <font color="5C878F">Master Client</font> is the underlying logic of the experiment and ultimately runs in the <font color="5C878F">Experiment Server</font>.

3. <font color="5185E8">Researcher</font> uploads the experiment, which consists of the <font color="5C878F">Master Client</font>, <font color="5C878F">Client</font>, and <font color="5C878F">Source Code</font>, to his local <font color="5C878F">GitHub</font> repository. 

4. <font color="5C878F">GitHub Client</font> syncs the contents of the local repository with the remote online <font color="5C878F">GitHub</font> repository. 

5. <font color="5185E8">Researcher</font> logs into the online <font color="5C878F">Researcher Dashboard</font> and selects an experiment to launch a trial. 

6. The <font color="5C878F">Popper Web Service</font> downloads the <font color="5C878F">Master Client</font> that corresponds to the selected experiment.

7. The <font color="5C878F">Popper Web Service</font> uploads this <font color="5C878F">Master Client</font> to the <font color="5C878F">Experiment Server</font>.

8. The <font color="5C878F">Popper Web Service</font> remotely starts the <font color="5C878F">Master Client</font> on the <font color="5C878F">Experiment Server</font> and connects it to the <font color="5C878F">Photon Server</font>, creating a trial. 

9. The <font color="5C878F">Popper Web Service</font> announces the trial to eligible <font color="DB563B">players</font> in the <font color="DB563B">Popper Subject Pool</font>.

10. Interested <font color="DB563B">players</font> log into the <font color="5C878F">Player Site</font>. 

11. The <font color="DB563B">Player Site</font> downloads the <font color="5C878F">Client</font> from the experiments repository on <font color="5C878F">GitHub</font>.

12. The <font color="DB563B">Player Site</font> opens the <font color="5C878F">Client</font> on each <font color="DB563B">player's</font> browser or phone. The <font color="DB563B">player</font> sees the game.

13. Each <font color="5C878F">player's Client</font> connects to the current trial running on the Photon Server.

14. The <font color="5C878F">Popper Web Service</font> establishes a connection with <font color="5C878F">Photon Server</font> via <font color="5C878F">Photon Client</font>. The trial begins.

15. The <font color="5185E8">Researcher Site</font> monitors the ongoing trial via <font color="5C878F">Photon Client</font>.

16. All events in the trial are recorded in the <font color="5C878F">Popper database</font>.

17. <font color="5185E8">Researcher</font> monitors the ongoing trial in his browser. Once the trial ends, <font color="5185E8">Researcher</font> reviews and approves subject payments.

18. The <font color="5C878F">Popper Web Service</font> posts payments to <font color="DB563B">players'</font> accounts. 


## <a name="DevelopmentTeam" id="anchor0">Development Team</a>


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