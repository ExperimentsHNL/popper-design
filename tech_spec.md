# Tech Spec 

## Table of Contents

-	[Introduction](#Introduction)

-   [popper-researcher](#PopperResearcher)

	-   [Authentication and Permissions](#AuthenticationAndPermissions)

	-	[Git and Github Integration](#GitAndGithubIntegration)

	-	[Experiment Creation](#ExperimentCreation)

-	[popper-deploy](#PopperDeploy)

-   [popper-windows-deploy](#PopperWindowsDeploy)	 

## <a name="Introduction" id="anchor4">Introduction</a> ##

Following are the tech specs for **Popper**.  Included is a description of the development process, style guidelines for contributing to the **Popper** source, and documentation for all features included in the current **Popper** release.

### Development Process

The development process extends from brainstorming a feature to closing bug tickets for that feature.  The development process is designed for sharing information between developers and non-developers, and for creating a comprehensive log of the development of a feature.  

It's extremely important to follow a rigorous development process in order to reduce the amount of time that's spent redeveloping features because of miscommunication between the developer and project manager, or readdressing bugs that were never fully fixed, etc.  The development process is defined as the interaction between a **Developer** and a **Project Manager**.  

It's important, even as **Popper** grows, to maintain a single line of communication between the development team and the **Project Manager**, who's in charge of communicating functional specs and aggregating information from many different sources, including: other non-developers, clients and advisors.

#### Process
1. A feature is brainstormed, either by a developer or a non-developer.  
2. Feature creator clones and branches the popper-feature repository and commits all notes, drawings or other informal documents to a new folder. 
3. Feature creator writes a [functional spec](http://www.mojofat.com/tutorial/) and commits it to the repository branch.
4. Feature creator hands off the spec to the **Project Manager**, who adds it to the Product Backlog.
5. **Project Manager** assigns the feature to a developer(s).  **Developer** should only be assigned one feature at a time. 
6. **Developer** pulls from the popper-feature repository and checks out the associated feature branch.
7. **Developer** writes a tech spec, including a time estimate, and commits it to the feature branch.
8. **Project Manager** approves tech spec.
9. **Developer** branches Popper source.
9. **Developer** builds feature.
10. **Developer** writes tests for critical methods.
11. **Developer** creates a new tag and merges back into master.
12. **Developer** pushes code to the staging environment.
13. **Project manager** tests feature by designing functional tests using [Selenium](http://seleniumhq.org/).
14. When tests pass, tag is pushed to production.
15. **Developer** adds an entry in the popper-design/tech_spec.md file for the feature.

##### Bug Fixes
1. When a bug is reported, **Project Manager** replicates it in a [Selenium](http://seleniumhq.org/) test.
2. **Developer** fixes bug.
3. When tests pass, **Project Manager** closes bug ticket..

#### Github Workflow
1. Clone the relevant repository that you'll be working in.
	- git clone git@github.com:Experiments/popper-**Service Repository**.git
2. Check out the development branch.
	- git checkout --track origin/development
3. Checkout a new branch named after your feature.
	- git checkout -b my_cool\_feature
4. Do work!
5. Make sure you're up to date with the latest from the remote repository.
	- git checkout development
 	- git pull
6. Roll your changes on top of the development branch.
	- git checkout my_cool\_feature
 	- git rebase -i development
7. Merge changes back into the development branch.
	- git checkout development
 	- git merge my_cool\_feature
8. Push changes to the remote repository 
	- git push origin development
9. Delete your feature branch 
	- git branch -d my_cool\_feature

### Style Guidelines

#### General Guidelines

All code should be written in accordance with the associated language/framework guidelines.  Most often, this will mean adhering to the [Ruby on Rails style guidelines](https://github.com/bbatsov/rails-style-guide), also found [here](http://pathfindersoftware.com/2008/10/elements-of-ruby-style/).

#### **Popper**-specific Guidelines

##### Configuration Variables
Configuration variables are stored with the Configuration class, in **config/configuration.rb**.

To set a configuration variable, add the variable name in **attr_accessible** in **config/configuration.rb**, then set the variable in an initializer class for a given environment, in **config/initializers/*.rb**, for the desired environment.

##### Linking to External URLs
When linking to an external resource, such as an OAuth authentication point, avoid linking directly to the resource from the view, rather, create a path in the routes file and use the path helper.

Like this:

**match "/blog" => redirect("http://example.com/blog"), :as => :blog**

Use the **blog_path** helper in your actions.

## <a name="PopperResearcher" id="anchor5">popper-researcher</a>

### <a name="AuthenticationAndPermissions" id="anchor5">Authentication and Permissions</a>

#### Description
Handles user login/creation/permissions.

#### Relevant Gems
cancan, authlogic, omniauth

#### Controllers
user_sessions_controller.rb, users_controller.rb, application_controller.rb

#### Models
ability.rb, user_session.rb, user.rb

#### Application Flow:
- New User Creation: Users/New -> Users/Create
	- Users/New
		- Call User.new
		- Render Form
	- Parameters:
		- First_name
		- Last_name
		- Email
 		- Username
		- Password
		- Password_Confirmation
	- Users/Create
		- Call User.new(params[:user[)
		- Check @user.valid?
		- @user.save

- User Login
	- Saves attempted page for redirect
	- User_sessions/new
		- UserSession.new
		- Render Form
	- User_Sessions/create
		- UserSession.new(params[:user_session])
		- If @user_session.save?
			- Redirect to homepage or desired page
		- Else
			- Renders User_sessions/new

- User Logout
	- User_sessions/destroy
		- @user_session.delete

#### Permissions
Permissions are handled with CanCan Gem and set in **models/ability.rb**.

- Researcher
	- Can access Experiments Controller
- Player

#### Notes
UserSession inherits from Authlogic Gem

### <a name="GitAndGithubIntegration" id="anchor5">Git and Github Integration</a>

#### Description
Links user to a Github account via OAuth2, adds them to the Experiments organization on Github with a personalized team, and creates a new private repository for that user

#### Relevant Gems
octokit, httparty

#### Controllers
user_sessions_controller.rb

#### Models
user.rb, (github.rb)

#### Application Flow
- If user needs a Github Access Token
	- Users/needs_github
		- Link to Github Oauth Endpoint: github\_authentication\_path
	- User\_sessions/github_callback
		- Call @user.github_authenticate(params[:code])
			- Call self.github_init(code)
				- POST code to retrieve access token
				- Save Github access token for user
			- Call self.github_create_user_team
      		- Call self.github_add_user_to_team
      		- Call self.github_create_organization_repo("#{self.username}'s New Experiment Repository")			
		- Handles Errors:
			- If User authenticates with Github but can’t create a team
			- If User has authenticated with Github but deleted team and can’t create a repo

#### Notes
Need functional/unit test coverage for this feature.

### <a name="ExperimentCreation">Experiment Creation</a>

#### Description
Allows users to create an experiment, associate it with a github repository, create an associated trial, and deploy the repo to the Windows farm.

#### Relevant Gems
octokit, httparty

#### Controllers
experiments_controller.rb

#### Models
experiment.rb, user.rb, (github.rb)

#### Application Flow
- Experiment Creation: Experiments/New -> Experiments/Create
	- Experiments/New
		- Call Experiments.new
		- Render Form
	- Parameters
		- Name
		- Description
	- Experiments/Create
		- Call Experiment.new(params[:experiment])
		- If @experiment.save?
			- Redirect to browse_repos_experiment_path
		- Else
			- Render form with associated errors
	- Experiments/Browse_repos
		- Render list of available repos
	- Experiments/Deploy
		- Call @experiment.deploy(params[:repo])
		- If @experiment.deployed?
			- Render success message
		- Else
			- Render browse_repos with error message

#### Critical Methods
- Experiment.rb:deploy
	- Sets deployed_at time to current timestamp
	- Creates a new Thread and posts a request to Sinatra service that handles repository cloning and upload
		- Eventually need to just clone the repository to S3, where it’s accessible by the windows server.  Alternatively might use EventMachine or Node.js for greater efficiency.
	- Returns true or false depending on deployment status
	
#### Notes
Need to better develop error handling for the asynchronous request to the sinatra server.

## <a name="PopperDeploy">popper-deploy</a>

### Trial Creation

#### Description
Clones a git repository from Experiments organization using Admin credentials and uploads it to the photon server.  

#### Relevant Gems
sinatra, net/ftp, httparty, octokit

#### Routes
GET /deploy (:username, :repo)

#### Application Flow 
- Receives Request
	- Calls:
		- system "git clone git@github.com:Experiments/#{params[:repo]}"
	- Tars the binaries folder (/binaries/) in the repository for SFTP transfer:
		- system "tar -cvf #{params[:repo]}/binaries/masterclient.tar #{params[:repo]}/binaries/masterclient.zip"
		- Tarring preserves the directory structure, so when extracting programmatically, /binaries/ will be nested in two other folders.
	- Uses Net/FTP to upload tarred binaries.
	- Makes a request to the Sinatra app located on the windows server to start the masterclient.exe file.  

## <a name="PopperWindowsDeploy">popper-windows-deploy</a>

### Deploy Masterclient

#### Description
Handles moving source files into an instance folder and starting the masterclient.

#### Relevant Gems
sinatra, 7zip, filezilla

#### Routes
POST /new (:instance, :id, :args)

#### Application Flow
- Receives Request
	- Extracts tar file in /library (where it was uploaded by the Sinatra app)
	- Extracts zipped binaries
	- Copies executable and webplayer to new instance folder
	- Calls 
		- system("start masterclient.exe #{params[:args]}")