# Popper Brief 

## Table of Contents

-	[Introduction](#Introduction)
	
-	[Platform Overview](#PlatformOverview)

-   [Development Team](#DevelopmentTeam)

-	[Unity Programmer Brief](#UnityProgrammerBrief)

-	[Web Developer Brief](#WebDeveloperBrief)

-	[Web Designer Brief](#WebDesignerBrief)	 

-	[Mobile FB Authentication](#MobileFBAuth)

## <a name="Introduction" id="anchor4">Introduction</a> ##

**Popper** is a behavioral experiments platform that empowers researchers in economics, psychology, sociology, and political science to create and conduct complex large-scale online experiments. 

### Role of experiments in the social sciences

 Social scientists are interested in studying human behavior. They develop theories to explain this behavior and conduct controlled experiments to test these theories. In order for a theory to be "testable", it must produce predictions (hypotheses) about human behavior that can, in principle, be proven wrong. Thus, the process of experimentation results in the falsification of inaccurate theories. 

### Classical experiments

Conducting controlled experiments in the social sciences is difficult. Unlike natural scientists, who often conduct their experiments with inanimate objects, social scientists experiment exclusively with live human beings. Human subjects cannot be forced to participate in experiments and can also quit an ongoing experimental trial at any point. For these reasons, researchers must pay human subjects to convince them to participate in and complete a trial. These trials are typically run in physical laboratories, where invited volunteer subjects engage in simple decision tasks for $15-25/hour--and sometimes more depending on their performance. 

This approach has three serious limitations: 

1. It is very expensive, requiring an equipped brick-and-mortar laboratory and significant subject payments that often exceed $500-1000 per trial. 

2. It is time-consuming and requires recruiting local human subjects more than a week in advance of the trial. 

3. Local subject pools are relatively small, so large-scale trials require using laboratories in multiple geographical locations.

In addition, the software used in physical labs to create and conduct experiments is very outdated. The most popular package, [z-Tree](http://www.iew.uzh.ch/ztree/index.php), was created in the University of Zurich in the late 1990s and hasn't been updated since then.

### Online experiments

In the last 2-3 years, researchers have started conducting experiments online, using subjects from various online labor markets, most notably [Amazon Mechanical Turk](http://mturk.com). This move has radically expanded the size of the available subject pool and decreased subject payments. Now, experimental subjects can participate in trials from the comfort of their own home rather than coming to a physical lab.

However, the move to online trials introduces several new challenges:

1. **Lack of software.** Most online trials have so far been technologically limited to survey-style tasks that do not involve realtime interaction between subjects. The researchers who do conduct multiplayer studies have had to write from scratch their own ad hoc software. No reusable framework capable of supporting multiplayer online trials is currently available on the market.

2. **Low comprehension rates of written instructions.** Online subjects frequently skim, or even ignore, written experimental instructions.

3. **High subject attrition rates.** Online subjects can quit a trial simply by closing a browser tab, with few consequences. This leads to very high attrition rates, especially in trials where subjects become bored. Even though subjects in a physical lab are also allowed to quit the trial at any moment, doing so usually involves an uncomfortable interaction with the researcher. 

4. **Lower degree of control over the experimental conditions.** Subjects can communicate with each other, collude, and cheat in other ways that undermine the [internal validity](http://en.wikipedia.org/wiki/Internal_validity) of the experiment.

### Popper

The goal of Popper is to address the above four problems. It seeks to streamline the process of creating complex and visually compelling multiplayer experiments. Through Popper, researchers will use professional game development tools, which include visual scripting and an extensive library of template game assets. Popper will also provide researchers with extensive subject monitoring capabilites to minimize the possibility of cheating and other runtime irregularities.

## <a name="PlatformOverview" id="anchor5">Platform Overview of Popper Platform</a>

Popper consists of four pieces: 

1. **Popper Software Development Kit (SDK)** -- a set of tools based on the Unity 3D game engine. The reseacher uses the Popper SDK on their local computer to design experiments in the form of short multiplayer games.

2. **Experiment Library** -- GitHub-based online repository used for storing and sharing source code, as well as binary files of developed experiments.

3. **Researcher Site** -- a website that the researcher uses to launch and monitor online trials based on experiments available in the **Experiment Library**.

4. **Player Site** -- a website that players (experimental subjects) use to browse and participate in trials launched by researchers.


Below is a diagram showing the general architecture of Popper. Click <a href="https://github.com/Experiments/popper-design/blob/master/images/popper_overview.png?raw=true" target="_blank">here</a> for a larger view.

<a href="https://github.com/Experiments/popper-design/blob/master/images/popper_overview.png?raw=true" target="_blank">![Popper Overview](https://github.com/Experiments/popper-design/blob/master/images/popper_overview.png?raw=true)</a>

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


### Unity Programmer

The Unity Programmer develops a robust Popper SDK based on Unity 3D, uScript, and Photon Networking. He/she works with us to create sample experiments that illustrate the capabilities of the SDK. 

Go to the [Unity Programmer Brief](#UnityProgrammerBrief). 

### Unity Designer

The Unity Designer creates graphical assets and templates of Unity scenes for researchers to use in their experiments. The designer also adapts existing games from the Unity Asset store for use in an experimental setting.

### Web Developer

The Web Developer works on the backend of the core web application that handles the launch, execution and monitoring of experimental trials.

Go to the [Web Developer Brief](#WebDeveloperBrief). 

### Web Designer

The Web Designer creates the logos, UI/UX, and front-end code for the Researcher Site and the Player Site. 

Go to the [Web Designer Brief](#WebDesignerBrief). 

## <a name="UnityProgrammerBrief" id="anchor1">Unity Programmer Brief</a> 

The Unity developer works on the Popper SDK and a set of stock games. The Popper SDK is a set of tools based on Unity 3D that researchers use to create online experiments. Specifically, it is a Unity package that includes the following components: 

#### 1. Third-party tools

- **uScript:** A visual scripting add-on for Unity developed by Detox Studios. Pending our distribution licensing agreement with Detox Studios, we may or may not bundle uScript with the Popper SDK. If we do not, users would download uScript from the Unity Asset Store.

- **iTween:** An open-source animation add-on for Unity.

- **Photon Unity Networking:** Unity-specific client for Photon Server developed by Exit Games/M2H. It is used to connect multiple players within the same experimental trial.

#### 2. Template frames

- **Template graphical assets:** Complete scenes and scene components, such as characters, props, sounds, animation, fonts, etc. that researchers can use to construct the front-end visual representation of their experiments. 

- **Editor Tools:** Customized set of tools that allow the researcher to manipulate visual assets and scenes; e.g., adapt a scene for a specific number of players by scaling the number of user-specific game objects. 

- **Client-side scripts:** Under-the-hood scripts and game controllers used to define the technical behavior of assets. Here, "technical" refers to behavior that *is not* relevant for the researcher to design the experiment and is hence not visible through uScript.

- **Text-only frame:** A bare-bones frame that features only text but no graphics rendered in real time. 

- **Tutorial creation system:** Tools for building short interactive tutorials explaining the rules of the experiment to subjects from within the visual frame. 

#### 3. Custom uScript nodes and canvases

- **Template uScript canvases:** Pre-made canvases that contain frequently used sequences of actions, such as the timing structure of a trial or the handling of subject payments. 

- **Client-side nodes:** Set of nodes available to researchers through the uScript palette that allow them to define the substantive behavior of visual frames. "Substantive" refers to behavior that *is* relevant for the researcher to design the experiment.

- **Server-side nodes:** Set of nodes available to researchers through the uScript palette that allow them to define substantive game logic.

#### 4. Metadata templates

The platform provides templates of metadata, which are included with each experiment. These metadata provide:

- A list (and default values) of input parameters that the game can accept, such as the number of players, number of rounds, compensation, etc.

- Full communication protocol between the client and server, including the list of permitted Remote Procedure Calls (RPCs).

- Full communication protocol between the Researcher Site and the server, including the list of permitted RPCs.

- An end-of-game report template that is updated with trial data by the Researcher Site at the end of the experiment. 

- Subject recruitment ad(s).

- A short game description (to be displayed in the Experiment Library).

#### 5. Local dashboard

The researcher should be able to test games locally within the Unity editor without having to create a remote server. This requires providing the researcher with an analog of the Researcher Site within Unity that makes it possible to create and run a sample trial. 

### Platform Documentation

Documentation for Popper will be Wiki-style and hosted on GitHub.

### Stock games

In addition to the Popper SDK, researchers will be provided with the following stock games to illustrate the capabilities of Popper.

- [Prisoner's dilemma](http://en.wikipedia.org/wiki/Prisoner's_dilemma)

- [Public goods game](http://en.wikipedia.org/wiki/Public_goods_game)

- [Dictator game](http://en.wikipedia.org/wiki/Dictator_game)

- [Ultimatum game](http://en.wikipedia.org/wiki/Ultimatum_game)

- [Trust game](http://en.wikipedia.org/wiki/Dictator_game#Trust_game)

- [p-Beauty context](http://en.wikipedia.org/wiki/Keynesian_beauty_contest)

- [Double-sided auction](http://en.wikipedia.org/wiki/Dutch_auction)

### General remarks

1. We would like for the size of the core Popper SDK to be as small as possible, leaving heavy graphical assets in separate packages available on-demand from GitHub.

2. Various limitations of uScript will become apparent as the developer works on the SDK. We have a very good relationship with Scott Blinn, co-founder of Detox Studios. They have been helpful in the past and would be willing to accomodate feature requests, bug reports, UI/UX suggestions, etc.

3. It is vital to take advantage of the graphical assets available in the Unity ecosystem. Accordingly, we need to streamline the process of importing professional third-party games, adding Photon networking, and integrating them with our uScript-based backend. 

4. We would like to keep the entry barrier for researchers as low as possible. Ideally, the Popper SDK should be compatible with the free version of Unity. At present, the Popper SDK relies on Unity Build API, which is only available in Unity Pro. We would like to find a way around this. 

5. We would like ot be able to deploy games to as many Unity-supported platforms as possible (Windows/Mac, Webplayer, Flash, Android, and iOS). Some of these platforms impose restrictions on networking; we would like to streamline the process of overcoming these restrictions.

## <a name="WebDeveloperBrief" id="anchor2">Web Developer Brief</a> ##

As mentioned in the Platform Overview section above, researchers and players interact with Popper through two separate interfaces: the Researcher Site and the Player Site. The former allows researchers to launch, execute, and monitor trials; the latter hosts games (trials) that players (subjects) play. The two sites are separate, with different domain names.

### Researcher Site 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_base.png?raw=true)

#### 1. Landing Page 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_landing.png?raw=true)

The purpose of the landing page is to introduce the researcher to the Popper Platform and encourage her to sign up. 

On this page the researcher should see:

- An introduction video (which we will create)

- Highlights of the platform (key features, advantages)

- A list of logos/shields of prominent clients using Popper

- A navigation panel with links to About, Experiment Library, Documentation (hosted externally on GitHub), and Sign up 

The navigation bar should be consistent and available (along with the Popper logo) throughout the entire website. If a researcher is logged in, the Sign Up link is replaced with their username, and they see an additional "Download" link. This link leads leads to one of our Documentation pages on GitHub, featuring the steps necessary to download the Popper SDK.

#### 2. Signup 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_signup.png?raw=true)

The Signup page allows the researcher to create a Popper account and go through the steps necessary to begin running experiments online. 

The Signup form should contain the following fields:

- Full name

- Email

- Affiliation

- Password


#### 3. Researcher Dashboard 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_dashboard.png?raw=true)

Once the researcher has completed signup, she will be taken to the Researcher Dashboard. Here, the researcher can see an overview of all her trials, as well as experiments that she is following. The Dashboard is divided into two main sections: the Feed and the list of their Trials.  

**Feed**

The Feed contains all important events associated with researcher's activity within Popper: creation of trials, completion of trials, pending payments, changes to the experiments that the researcher follows on GitHub, etc.

To clarify, the word **experiment** refers to the software (source code and binary files) created by the researcher on their local computer and stored in the Experiment Library on GitHub. The word **trial** refers to a particular run of an experiment, initiated by a researcher through the Researcher Site.

Researchers may choose to run trials using experiments that other researchers have already designed and made publicly available. The idea is for researchers to be able to share experiments with each other. 

Researchers often hire research assistants to run trials of their experiments. These research assistants would not be involved in designing the experiment and would only initiate and monitor trials.

**List of Trials**

Each trial on this list should be accompanied by the following information:

- Name of the underlying experiment

- Trial name

- Status (e.g. waiting for players, in progress, completed, error)

- Duration since start


#### 4. Experiment Library 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_library.png?raw=true)

The Experiment Library includes a list of all available experiments. We plan to launch with six stock experiments, each of which can be run with a different frame. The experiments should each be accompanied by an appropriate image, which we will provide. 

Two audiences are served by the Experiment Library. 1. Users without an account can browse the Library, but cannot initiate a trial. If they attempt to do so, they are prompted to create an account. 2. Researchers with an account can use the Experiment Library to select an experiment with which to launch a trial.

The list of available experiments is generated dynamically by the web application. It looks up GitHub repositories with experiments to which the user has access, and displays formatted descriptions of those experiments based on the metadata contained in corresponding  GitHub repositories.

We would like to encourage researchers to share details about the experiments that they create with the Popper scientific community. Relevant details include screenhsots, the title of the experiment, a list of available input parameters, etc.

A clear link next to the experiment allows the researcher to "Create Trial".

#### 5. Create Trial 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_trial.png?raw=true)

Once the researcher selects an experiment, she is shown a dynamically constructed form with the list of input parameters that the experiment accepts. Just like descriptions of experiments in the Library, this list of acceptable input parameters is taken from the metadata that accompanies the source code of the experiment. Typically, these parameters would include the necessary number of players, initial endowments of players, an exchange rate from in-game points to dollars that the subject receives, and the demographics of an acceptable subject pool.

Again, researchers without an account cannot access this page and will be redirected to the Signup page instead. 

#### 6. About 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_about.png?raw=true)

Just a stock about page using the same template as the Landing Page.

#### 7. Researcher Profile 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_profile.png?raw=true)

The Researcher Profile consists of the information that the researcher provided during the signup 
process as well as privacy settings, payment method, and linked accounts (GitHub, Facebook, and Twitter).

This page also contains the history of all trials ever launched by the researcher.

#### 8. Monitor Trials 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_monitor.png?raw=true)

By default, upon creating a trial, the researcher is taken to the monitoring page of this trial. Alternatively, the researcher can find out more information about any trial displayed in the Trial List in the Researcher Dashboard by clicking on the trial. This also takes her to the Monitor Trials page. 

The exact layout of the Monitor Trials page is dynamically constructed based on metadata accompanying the experiment. The metadata describes what kinds of events can happen and what kind of data about the trial will be available to the researcher during runtime. Typically, the monitoring page displays trial status, the list of players (researcher should be able to click on individual players and review their profiles), realtime choices made by the players, the round number, and players' earnings.

Once the trial is over, the researcher can see and manually approve all pending payments to players, still on the monitoring page. The researcher can also download the complete log of the game in CSV format.


### Player Website 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_base.png?raw=true)

#### 1. Signup 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_signup.png?raw=true)

Players will not be able to see available games (trials) unless they are signed in. We need to know precisely who is reviewing available trials. For this reason, the signup page is the landing page of the Player Website. Barriers to entry for the player should be minimal, especially since the player is most likely already arriving from an external site (Amazon Mechanical Turk or oDesk). The player should thus be able to create an account using an existing Facebook or Twitter account. The signup page should also be miminalistic in terms of data gathered from the player, asking only for a username, password, and the player's age. More in-depth demographic information will be gathered later, once the player has created an account--perhaps on a separate page, using the same template. This information will be used to determine which trials are visible to the player in the Lobby (2). 

Players who already have an account will use this page to log in. 

#### 2. Lobby 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_lobby.png?raw=true)

Players who are visiting the site directly without having pre-selected a game to play will be take to the lobby to browse games (ongoing trials) for which they meet eligibility requirements. Sometimes, researchers will restrict participation in their trials by age, gender, geographic location, connection speed, or other factors. The graphics and UI/UX should compel the player to stay on the website to play as many games as possible. We envision perhaps a screenshot of each game to accompany a link to each of the games. Basic information also accompanies each game visible to the player in the lobby: pay, trial end date, number of current players, and a description of the game itself. All this information is dynamically pulled by the web application from the corresponding metadata on GitHub.

#### 3. Game 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_game.png?raw=true)

The player plays the game on this page. The game is embedded as an iframe, and its design is the responsibility of the researcher.

#### 4. About 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_about.png?raw=true)

Basic About page, perhaps reusing the same template as the Signup page. 

#### 5. Player Profile 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_profile.png?raw=true)

The player can view his history of games on the profile page, as well as manage his account 
information and privacy settings. 


## <a name="WebDesignerBrief" id="anchor3">Web Designer Brief</a> ##
As mentioned in the Platform Overview section above, researchers and players interact with Popper through two separate interfaces: the Researcher Site and the Player Site. The former allows researchers to launch, execute, and monitor trials; the latter hosts games (trials) that players (subjects) play. The two sites are separate, with different domain names.

### Researcher Site 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_base.png?raw=true)

#### 1. Landing Page 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_landing.png?raw=true)

The purpose of the landing page is to introduce the researcher to the Popper Platform and encourage her to sign up. 

On this page the researcher should see:

- An introduction video (which we will create)

- Highlights of the platform (key features, advantages)

- A list of logos/shields of prominent clients using Popper

- A navigation panel with links to About, Experiment Library, Documentation (hosted externally on GitHub), and Sign up

The navigation bar should be consistent and available (along with the Popper logo) throughout the entire website. If a researcher is logged in, the Sign Up link is replaced with their username, and they see an additional "Download" link. This link leads leads to one of our Documentation pages on GitHub, featuring the steps necessary to download the Popper SDK.

##### Logo

1. The Popper Platform is named after [Karl Popper](http://en.wikipedia.org/wiki/Karl_Popper), a major philosopher of science in the 20th century, who established the modern practice of hypothesis testing. Given that the work "Popper" has multiple meanings, it is important for us that the logo conveys a clear association with Karl Popper, and is not confused with the action of "popping" or drugs. We would prefer to have an stylized image of Karl Popper as part of the logo.

2. Popper will be used by social scientists, not natural scientists. All images and logos should avoid any allusions to the natural sciences, such as test tubes, atoms, microscopes, as well as brains, light bulbs, etc. 

3. The Popper logo should work with both a dark and light background since it will be used both on the site (which will probably be light-colored) and within the Unity/uScript environment (which is dark).


#### 2. Signup 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_signup.png?raw=true)

The Signup page allows the researcher to create a Popper account and go through the steps necessary to begin running experiments online. 

The Signup form should contain the following fields:

- Full name

- Email;

- Affiliation;

- Password.


#### 3. Researcher Dashboard 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_dashboard.png?raw=true)

Once the researcher has completed signup, she will be taken to the Researcher Dashboard. Here, the researcher can see an overview of all her trials, as well as experiments that she is following. The Dashboard is divided into two main sections: the Feed and the list of their Trials.  

**Feed**

The Feed contains all important events associated with researcher's activity within Popper: creation of trials, completion of trials, pending payments, changes to the experiments that the researcher follows on GitHub, etc.

To clarify, the word **experiment** refers to the software (source code and binary files) created by the researcher on their local computer and stored in the Experiment Library on GitHub. The word **trial** refers to a particular run of an experiment, initiated by a researcher through the Researcher Site.

Researchers may choose to run trials using experiments that other researchers have already designed and made publicly available. The idea is for researchers to be able to share experiments with each other. 

Researchers often hire research assistants to run trials of their experiments. These research assistants would not be involved in designing the experiment and would only initiate and monitor trials.

**List of Trials**

Each trial on this list should be accompanied by the following information:

- Name of the underlying experiment

- Trial name

- Status (e.g. waiting for players, in progress, completed, error)

- Duration since start


#### 4. Experiment Library 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_library.png?raw=true)

The Experiment Library includes a list of all available experiments. We plan to launch with six stock experiments, each of which can be run with a different frame. The experiments should each be accompanied by an appropriate image, which we will provide. 

Two audiences are served by the Experiment Library. 1. Users without an account can browse the Library, but cannot initiate a trial. If they attempt to do so, they are prompted to create an account. 2. Researchers with an account can use the Experiment Library to select an experiment with which to launch a trial.

The list of available experiments is generated dynamically by the web application. It looks up GitHub repositories with experiments to which the user has access, and displays formatted descriptions of those experiments based on the metadata contained in corresponding  GitHub repositories.

We would like to encourage researchers to share details about the experiments that they create with the Popper scientific community. Relevant details include screenhsots, the title of the experiment, a list of available input parameters, etc).

A clear link next to the experiment allows the researcher to "Create Trial".

#### 5. Create Trial 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_trial.png?raw=true)

Once the researcher selects an experiment, she is shown a dynamically constructed form with the list of input parameters that the experiment accepts. Just like descriptions of experiments in the Library, this list of acceptable input parameters is taken from the metadata that accompanies the source code of the experiment. Typically, these parameters would include the necessary number of players, initial endowments of players, an exchange rate from in-game points to dollars that the subject receives, and the demographics of an acceptable subject pool.

Again, researchers without an account cannot access this page and will be redirected to the Signup page instead. 

#### 6. About 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_about.png?raw=true)

Just a stock about page using the same template as the Landing Page.

#### 7. Researcher Profile 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_profile.png?raw=true)

The Researcher Profile consists of the information that the researcher provided during the signup 
process as well as privacy settings, payment method, and linked accounts (GitHub, Facebook, and Twitter).

This page also contains the history of all trials ever launched by the researcher.

#### 8. Monitor Trials 

![Image](https://github.com/Experiments/popper-design/blob/master/images/rworkflow_monitor.png?raw=true)

By default, upon creating a trial, the researcher is taken to the monitoring page of this trial. Alternatively, the researcher can find out more information about any trial displayed in the Trial List in the Researcher Dashboard by clicking on the trial. This also takes her to the Monitor Trials page. 

The exact layout of the Monitor Trials page is dynamically constructed based on metadata accompanying the experiment. The metadata describes what kinds of events can happen and what kind of data about the trial will be available to the researcher during runtime. Typically, the monitoring page displays trial status, the list of players (researcher should be able to click on individual players and review their profiles), realtime choices made by the players, the round number, and players' earnings.

Once the trial is over, the researcher can see and manually approve all pending payments to players, still on the monitoring page. The researcher can also download the complete log of the game in CSV format.


### Player Website 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_base.png?raw=true)

#### 1. Signup 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_signup.png?raw=true)

Players will not be able to see available games (trials) unless they are signed in. We need to know precisely who is reviewing available trials. For this reason, the signup page is the landing page of the Player Website. Barriers to entry for the player should be minimal, especially since the player is most likely already arriving from an external site (Amazon Mechanical Turk or oDesk). The player should thus be able to create an account using an existing Facebook or Twitter account. The signup page should also be miminalistic in terms of data gathered from the player, asking only for a username, password, and the player's age. More in-depth demographic information will be gathered later, once the player has created an account--perhaps on a separate page, using the same template. This information will be used to determine which trials are visible to the player in the Lobby (2). 

Players who already have an account will use this page to log in. 

#### 2. Lobby 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_lobby.png?raw=true)

Players who are visiting the site directly without having pre-selected a game to play will be take to the lobby to browse games (ongoing trials) for which they meet eligibility requirements. Sometimes, researchers will restrict participation in their trials by age, gender, geographic location, connection speed, or other factors. The graphics and UI/UX should compel the player to stay on the website to play as many games as possible. We envision perhaps a screenshot of each game to accompany a link to each of the games. Basic information also accompanies each game visible to the player in the lobby: pay, trial end date, number of current players, and a description of the game itself. All this information is dynamically pulled by the web application from the corresponding metadata on GitHub.

#### 3. Game 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_game.png?raw=true)

The player plays the game on this page. The game is embedded as an iframe, and its design is the responsibility of the researcher.

#### 4. About 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_about.png?raw=true)

Basic About page, perhaps reusing the same template as the Signup page. 

#### 5. Player Profile 

![Image](https://github.com/Experiments/popper-design/blob/master/images/pworkflow_profile.png?raw=true)

The player can view his history of games on the profile page, as well as manage his account 
information and privacy settings. 

## <a name="MobileFBAuth" id="anchor4">Mobile FB Authentication</a> ##

Pass a hash to `/mauth/callback` that has:

-	uid

-	token

-	expires

-	expires_at

-	email
