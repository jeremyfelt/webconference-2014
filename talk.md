# Managing the Environment

Hello everyone. Welcome to “Managing the Environment”

## @jeremyfelt

My name is Jeremy Felt. I'm a senior WordPress engineer with University Communications at Washington State University. I moved form Portland, OR to Pullman, WA about a year ago to fill this position and have been having a great time working for higher ed. We're working on building out a nice publishing platform for everyone at the University based on WordPress. All of our work is open source. If you're interested in collaboration of any kind, find me.

## the future friendly web

Before we get into things, I want to address how managing environments fits with the tagline on this year’s Web Conference.

“The Future Friendly Web”

That’s a pretty broad statement, which is useful because it can generate broad conversation. In fact, it's possible that everyone in this room has a different way of defining “future friendly” in this context.

One thought may be to build the web in a way so that when left untouched for years, it will still work. Browsers will change, standards will change, but that piece of content you put on the web continues to serve its purpose.

Another possible way of thinking is that a future friendly web is one that changes when you want it to.

## the future friendly web changes when you want it to

So often our hands are tied by factors out of our control. Whether it be internal politics or learning curves or large meetings that make it hard to come to decisions. Many things can be stubborn in the way of progress.

The longer things sit, the more things change around them. The more things change around them, the harder it is to change when the time comes.

On the other hand, when continuous changes are being made, there is no easy opportunity to prevent change from happening or to be scared of what a large rewrite would look like if you are constantly shipping.

## Rapid Incremental Improvements

To constantly ship, we’ll should rely on rapid, incremental improvements.

Many small enhancements will go unnoticed by many people. Large features will be broken down into smaller pieces that can be tested individually before being combined as part of a major effort. Bugs introduced into the system will have smaller effects.

For this to work, a clean and clear workflow must exist. Development should be a mirror of production that everyone can work with.

## Workflow... Development -> Production

Defining a workflow is the most important part.

Everything we’re covering here involves buy-in from your team (and from you).

In order for everyone to stay sane, an established workflow must exist. Even if you are the sole developer, designer, and content creator for a site, you’ll benefit from a solid workflow.

## Development vs Production

Let's assign some quick definitions to these environments.

Development is local and individual. You can break it at will. There are extra debug tools, build tools, and deploy tools. Everything you are working with is usually at the bleeding edge of your project rather than in a long term stable state.

Production is central and shared. It is clean and if you break it, you buy it.

A development environment allows everyone to do whatever they want in the common goal of maintaining a stable and happy production environment.

I'm purposely leaving out staging at this point, as it introduces additional complexities. I personally think that content can be staged in production in most cases. That said, if you need a staging area for QA, that should exist as part of the workflow and likely be as close to production as possible.

Create in a development environment and push to a production environment.

## Who are you?

Ok. Now that we’ve laid some of the ground rules, let’s back up again.

Who in the room would describe themselves as a developer?

Designer?
Content creator?
Manager?

We’re all here as part of the greater web community, interested in finding, creating, and playing the roles necessary to making and maintaining a future friendly web. Though this talk on managing the development environment is targeted at developers who want to explore ways to expand workflow, the methods and lessons within very much apply to everyone.

In fact, the more members of your team that can be involved in the push from development to production, the better. This allows that many more incremental improvements without a central gatekeeper.

## What does this entail?

Ok. I’m getting to the point.

What does all of this entail? How do you create a workflow that gets things from development to production in a painless, carefree manner?

There are 4 parts. Each part shares 2 key pieces.

Parts: Version Control, Provisioning, Deployment, Testing

Throughtout these four parts, as a whole and individually, we should focus on two things.

Pieces: Establish a workflow. Include everyone.

Let's get into it.

## Version Control

The most important part of a development workflow is version control. This will be used to keep track of your code and likely some of your processes. At WSU we're currently using it to track our platform code, the provisioning for our servers, and our deployment scripts that get things to production.

-----smiley------smiley------smiley-------sad Graph with a line back.

Not only does verion control give you the ability to maintain a log of what has happened—something you can reference when trying to determine when a bug was introduced or what the reasoning for an approach was—it allows you to rollback to any point in the history of your project and get a view of how exactly things worked.

Before you can get started with version control as part of your workflow, you should decide which type of version control to use.

Version control has a storied history that's completely worth reading. The two most popular packages now are Git and SVN.

### Git or SVN

Does anyone in the room already use Git? How about SVN? Any other types of version control in use?

Git and SVN are the big ones, and the choice should be made carefully and early. Once you choose one, that becomes the right answer. Embrace it.

Of course, you aren't really choosing between Git and SVN at this point. Your choosing between distributed and centralized.

### Distributed or Centralized

Distributed version control, which Git is, means that everyone on your team has a full copy of the repository's history's checked out to their machine. They can create branches and commit code and screw things up and fix them without anyone else ever seeing the work. They can also share the work constantly through the use of a common repository such as github. As multiple people contribute multiple branches of code, things can be merged together to form a common history that creates the product,

Centralized version control, SVN, is completely different. There is one repository. Everyone checks out a copy of the source from a specific point, but any commits must be pushed back to that central location so that everybody always has access to the same thing.

There arguments for and against both models. While centralized version control can make things difficult to work with as you rely on that central connection, decentralized can also create scenarios where large swaths of work are done as lone developers—possibly unwilling to show our unfinished work.

Having used both fairly extensively, I'm a bigger fan of the distributed model. If for no other reason than having the ability to commit code anywhere and to really go down an experimental path without having to worry if I'm affecting the work of others,

### Establish a Workflow

Once you choose a version control system, you'll want to establish a workflow.

* How are branches named?
* What is the master branched used for?
* When do we tag?
* Do we use semantic versioning or something else?
* Who has commit access?

All of these questions can help your team establish a workflow to follow for your projects.

### Simple example workflow

The first example is simple, and my favorite for most projects. There is a relatively stable master branch off which production versions are created with tags. Work is done on feature or bug branches and then merged into master when tested and ready.

This can mean that the master branch is constantly being updated. It also means that production is constantly changing. This can be helpful when you're goal is to keep pushing the platform forward, as features are always hitting and bugs are always being fixed.

### More of a standard workflow

http://nvie.com/posts/a-successful-git-branching-model/

### Include everyone

Your version control is only as good as how you use it. It will benefit everyone on your team if everyone became familiar with the concepts and started using it for projects. Being aware of how code gets to production is the first step. Having a method to contribute to that flow is the second.

This gets a bit tough. The best way to use Git is at the command line. If you're on GitHub, a cross platform app is available, but does a very poor job of encouraging best version control practices. I would recommend teaching some command line basics first so that everybody is on the first page together. It would be helpful to aid in creating workflows using other apps as well.

## Provisioning

Provisioning is the next important part of a development workflow. This is often the one that stands out a bit as something not every developer is familiar with.

Provisioning allows us to describe the state of a machine. Every time a fresh box is booted in production and development, this state is applied. When done right, it gives everybody on the team access to a local environment that provides everything we expect from production.

This means fewer lost hours tracking down caching bugs or trying to troubleshoot how a site is operating in Nginx while we run Apache on our local machines.

This does depend on the structure of your web team and how it alings with IT. If everybody is on board with the idea, it makes both server management and development an easier task. In many cases, it would be music to a system admin's ears to hear that you're interested in provisioning a local environment to match production.

Of course, the best reason to formalize your provisioning?

### Version Control

Formal provisioning allows you to version control your environment. And this is so useful.

This is actually the first thing I started with when building the WSUWP Platform. I needed a server before I could write code for it, so I started with provisoning before a line of code was written.

Now, over time I can see how the server configuration has changed. When we upgraded from Nginx 1.6 to 1.7. When that strange issue with PHP 5.5.12 required a change in www.conf.

Which brings up a good point. Version control may not be the best reason. The best reason may be that by having a local version of production provisioning, I was able to realize that PHP 5.5.12 caused an issue with our curreng server configs on my local machine - this MBA - before anything was accidently deployed to production.

I could go on, it really is cool stuff.

### How to create production

The first step to creating a production environment, which will also turn into your development environment is to pick a provisioner. There are many out there, but a few stand out.

As with many things, the one you pick is likely the right answer. As long as you establish your workflow and commit to it.

#### Salt

* "Salt delivers a dynamic communication bus for infrastructures that can be used for orchestration, remote execution, configuration management and much more."
* I clicked with Salt almost immediately, where as I was always confused when digging into Puppet and Chef. Granted, I was also looking for some instant gratification, so your mileage may vary. I really do enjoy the YAML style configuration offered by Salt.
* It is an exteremly active open source project, so you'll want to keep an eye on some changes. I think it has grown a bit more stable as of late.

#### Puppet

* "Puppet Open Source is a flexible, customizable framework available under the Apache 2.0 license designed to help system administrators automate the many repetitive tasks they regularly perform."
* A bunch of devops use and enjoy Puppet. I haven't had a chance to wrap my mind around the structure completely. It is different in that states are described with more of a Puppet specific language.

#### Chef

* "Chef is a systems and cloud infrastructure automation framework that makes it easy to deploy servers and applications to any physical, virtual, or cloud location, no matter the size of the infrastructure. "
* Chef is the one I have the least experience with. Per Chef, they approach infrastructure as code. Configuration, as far as I understand it, is done in Ruby. I have a feeling that if you're strong in Ruby, you'll have no problems adapting to Chef.

#### Others

There are others, Ansible comes to mind immediately as something that was very easy to get up and running with. http://en.wikipedia.org/wiki/Comparison_of_open-source_configuration_management_software

And there's always bash scripting. When in doubt, have common tasks scripted out so that you can boot up a server and run a few commands rather than walking through the full install every time. A provisioning method is better than no provisioning method. Salt, Puppet, Chef, and the others can involve some time to get familiar with and get buy-in.

### How this mirrors development

So that was a bunch of info on getting a production environment up and running with provisioning scripts. How does that relate to development?

#### Vagrant

This is where magic comes in.

Vagrant is MIT licensed open source software for “creating and configuring lightweight, reproducible, and portable development environments.”

Vagrant gives you a method to apply provisioning scripts to a virtual machine that exists on your local computer. Through virtualization software such as VirtualBox, this machine can live for years or be wiped out within minutes—all without affecting anything on your actual system.

The most important part—both Vagrant and VirtualBox are cross platform. This lowers barriers for any member of your web team as OSX, Windows, and Linux users can develop in the same common environment.

### Establish a Workflow

As with version control, having a formal provisioning process is most useful when a workflow has been established.

* When should provisioning run on production?
* How long should provisioning be tested in development?
* Should provisioning include debug tools in development?

### Example Workflow

So my daily workflow, almost the first thing I do when I walk in in the morning, is:

`vagrant up`

This fires my virtual machine up and starts all of the services I need to develop locally.

I subscribe to updates on packages like PHP and Nginx, so I'm often aware when a new release is available and if it includes updates that we should look at for production. At this point, I'll run `vagrant provision` to have my local machine go through the same provisioning that would occur on production.

If this all completes successfully and the project is working as expected, then I connect to the production machine and issue two commands.

1. Pull down the latest provisioning configuration.
2. Run Salt.

Really, this could be simplified into one step and it could automatically happen based on a trigger in our version control setup, but I'm still in the phase of paying close attention.

What's beautiful is that even when doing a large update - like recompiling Nginx 1.7.1 from source last week - the web server only blips for a couple seconds during provisioning.

And if something was to blow up completely, only a few commands and about 5-10 minutes stand in the way of having a working server up and running again.

### Include Everyone

Just like with version control, there's a learning curve here. But just like version control, the more the team is familiar with the workflow, the larger benefit it will have on the team as a whole. It's kind of like knowing where your food comes from.

Being aware of the process, possibly from browsing documentation, is the first step. How the server gets to be how it is and how we mimic this locally.

The next step is getting everyone working on a virtual machine rather than on production via FTP or through MAMP or XAMPP or some other development environment. I'm happy to have a crew of people using Vagrant now at WSU that avoided the terminal at all costs before. As long as you're familiar with some of the basics and have a support path available to you, everything is possible.

## Deployment

Deployment is the act of getting things into production. In our case, it's specifically getting things that have been tagged as stable in our version control system into production.

There are so many ways of doing this, so the best answer is often a combination of things depending on where your code is stored and what is required as part of a build process.

### Painless, then seamless.

First strive toward making it painless. Have a process laid out where a happens, then b happens, and then c causes d to happen. Once it feels like it's getting painless, start working so that it's seamless. Try to merge steps b, c, and d into a as appropriate. It's a happy day when you can trigger one action that sets off the series of tasks and deploys your code to production.

### Git hooks

Git has a series of hooks available in your project's `.git/hooks/` directory. There are a couple ways you can go here.

A pre-receive or post-receive hook on the server will allow you to specify commands to run on the server whenever a push is made to that repository.

A pre-commit or post-commit hook on your local machine will allow you to specify commands that will run locally.

### Grunt

Grunt is a task manager. This can be extremely useful for defining a series of tasks that need to be processed in order to build either a development or production version of your project.

This could be used in combination with Git hooks or on its own entirely. Typing `grunt production` may compile or build all of the files you need in production and then route them to the proper location.

### Fabric

"Fabric is a Python library and command-line tool for streamlining the use of SSH for application deployment or systems administration tasks."

Really, it's a nice way of defining a few bash tasks in python so that you can do things locally like `fab push_production` and have it just work.

This is powerful in that it provides some easy methods for connection to a remote server over SSH as a specific user or with SUDO.

If you find yourself writing a lot of Bash scripts as part of your deploy process, you may want to look into Fabric as a way to manage them.

### Version control

And of course, just like your code and just like provisioning, keep all of your deployment scripts under version control as much as possible. It's so nice to know when things have changed or to have a record available for going back to see why things were changed.

### Rollback Ability

With everything version controlled, especially in your code and provisioning, the concept of a rollback becomes easier to grasp. This is the goal to strive for after making your deployment painles and seamless—picking a point in a project's history and deploying to that moment.

You'll likely have trouble going too far back with provisioning, as software packages on servers would be really annoying to go back more than a version or to. But your code is more than likely flexible enough to handle that shift backwards.

Ideally, it should be possible to tag version 1.0.1 and have it appear in production. And if something catastrophic happens and you need to revert, it should be possible to issue one command and have production go back to 1.0.0 or 0.9.5 or whatever you've specified.

The only concern outside of code at this point becomes database and content related.

### Establish a Workflow

And again. Establish a workflow.

* Who can deploy code to the server?
* When should code be deployed to the server?
* What should be done to ensure deployment was successful?
* How can we rollback?

### Example Workflow

I'm starting to reach the point of painless in our configuration. I think seamless is close, and rollback will be available soon for some things.

Right now deployments for our WSUWP Platform occur in two different ways.

#### Theme deployment via GitHub webhook

First, any WordPress themes that we have available in public GitHub repositories are deployed whenever a new version is tagged. We developed a WordPress plugin that manages the webhook calls from GitHub and fires off the scripting on the server necessary for getting theme files in the right place.

The plugin also logs each of these deployment instances so that we have a history of what has happened and who has deployed. At this point, anybody on the team has the ability to deploy new changes to any themes on the platform.

We're very close on rollback ability here as the script is configured to checkout a specific tag from version control.

#### WSUWP Platform deployment via pre-receive hook

The platform itself is currently deployed through a pre-receive hook, though I do create a new tag each time that it is deployed.

Everyone's local repository contains an "origin" remote that points to GitHub and a "deploy" remote that points to the server. `git push origin master` pushes the master branch to GitHub and `git push deploy master` initiates a push to the master branch on the server.

Because this is a pre-receive hook, I have a bare git repository on the server that catches the request and fires off a bash script to pull down the latest changes before running Grunt to build the various themes and plugins that we're using into something that then gets put into production.

We're very close to having this work on the same system themes are on. So in the end, the deploy system will have the ability to deploy itself, which seems pretty cool.

### Include Everyone

The best deployment tools are those that everyone on your team can use. One of the common sticking points that I've run into is how much everybody enjoys cowboy coding. I've made changes to my CSS file, things look good, and I want to drag it to my shared drive on the server so that it's live.

This just hurts.

At the same time, it's painless for the deployer. Possibly painful for everyone at a later time, but that moment is painless.

If possible, integrate deployment steps into other parts of the workflow. As I showed in the example workflows, I've found it extremely useful to push minor tagged releases in version control as production ready. This lets anyone use either the command line or the tools available through GitHub to deploy code to the server.

## Testing

So I'm not going to talk about test driven development as it's not something we're currently taking advantage of.

This is your standard testing. Being aware of when things are deployed to production and how to determine if problems have been created. After a while there are so many different possibilities hanging out there throughout the sites of the University that nothing beats actual page loads for testing results.

### Keep an ear to the ground

Keep your eyes and ears open. If you deploy a new version of a project and then run out to get coffee and somebody mentiones something they just noticed, run it through your mental checks as something you may have possibly caused. This is unlikely to happen, though becomes more likely as more time passes after a deploy.

### Watch THOSE sites

Those sites exist. The ones that you know are high visibility flagship projects or high funded initiatives. There should be a handful of sites that you have ready to load any time its applicable. Push out a change to the platform, load those sites. Brief power outage, load those sites.

There are some pretty cool tools out there for automated visual regression testing that I'd like to harness in the future to have a constant eye on those sites. Nothing beats your eyes though.

### Be a constant user

And because nothing beats your eyes, be a constant user.

If you can be involved in the day to day use of the type of site you're creating, then you'll have an easier time finding bugs before they come up for others and for detecting features that you may want to start planning for now.

### Include Everyone

And of course, especially with testing, include everyone. This doesn't mean only members of your team, but everyone in the University. Make sure that the channels of communicaton are clear so that both minor and major issues can make their way to you as necessary.

One of the best things we've done recently at WSU is open lab hours on Friday mornings. I read this great article by Michelle Tarby (http://higheredsolo.com/newmodel/) on the open labs they started at Le Moyne College in Syracuse and fell in love with the idea immediately. We've had 5 sessions and each has generated some great discussion about current features, desired features, possible bugs, and the web in general. I take notes throughout the session and then post recaps to give everyone an idea of what we covered. http://web.wsu.edu/openlab/

If nothing else, this makes the web team more approachable. It gets everybody comfortable with the things that we're doing centrally and allows us to continue pushing changes.

## Trust

We've covered Version Control, Provisioning, Deployment, and Testing. Each of these have shared a common thread - establish a workflow and then include everyone.

Doing this creates trust within and outside your team. This trust is important in order to maintain a project flow that is always changing.

If you can get comfortable - and if you can get others comfortable - with the process used to create and push code... rapid, incremental improvements will follow.

## Thank You!
