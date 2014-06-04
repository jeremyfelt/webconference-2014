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

## what does this entail?

Ok. I’m getting to the point.

What does all of this entail? How do you create a workflow that gets things from development to production in a painless, carefree manner?

There are 4 parts. Each shares 2 key pieces.

Version Control, Provisioning, Deployment, Testing

Throughtout these four parts, as a whole and individually, we should focus on two things.

Establish a workflow. Include everyone.

Let's get into it.

## Version Control

The most important part of a development workflow is version control. This will be used to keep track of your code and likely some of your processes. At WSU we're currently using it to track our platform code, the provisioning for our servers, and our deployment scripts that get things to production.

-----smiley------smiley------smiley-------sad Graph with a line back.

Not only does verion control give you the ability to maintain a log of what has happened—something you can reference when trying to determine when a bug was introduced or what the reasoning for an approach was—it allows you to rollback to any point in the history of your project and get a view of how exactly things worked.

Before you can get started with version control as part of your workflow, you should decide which type of version control to use.

The two most popular packages now are Git and SVN.

### Git or SVN

Does anyone in the room already use Git? How about SVN? Any other types of version control in use?

Git and SVN are the big ones, and the choice should be made carefully and early. Once you choose one, that becomes the right answer. Embrace it.

Of course, you aren't really choosing between Git and SVN at this point. Your choosing between distributed and centralized.

### distributed or centralized

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

Provisioning is another very important part of a development workflow, and this is often the one that stands out a bit as something not every developer is familiar with.

Provisioning allows us to describe the story of the machine every time a fresh box is booted. And this is the key—provisioning can happen in production AND in development. When done right, it gives everybody on the team access to a local development environment that comes with everything we expect from production.

This means no more hours lost to tracking down caching bugs, or trying to find a matching config in nginx while we run Apache on our local machine.

Much of this also depends on the structure of your web team and how it aligns with IT at the University. Hopefully everybody can get on board with the idea, as it makes server management and development an easier task.

Having access to a server provides great power. You can install whatever you want to get the job done. While this is cool, it doesn't do much for us if we have to install all of the server software every time that we boot the machine.

And the best reason?

### Version Control

Formal provisioning allows you to version control your environment.

This is actually the first thing I started with when building the WSUWP Platform. I needed a server before I could write code for it.

### How to create production

The first step to creating a production environment, which will also turn into your development environment is to pick a provisioner. There are many out there, but a few stand out.

Salt - 

Puppet - 

Chef - 

Bash scripting.

When in doubt, a provisioning method is better than no provisioning method. Salt, Puppet, Chef, and the others can involve some time to get familiar with and get buy-in. Nothing hurts though, so having a list of bash scripts available would go along way.

### how this mirrors development

#### vagrant

### Establish a Workflow

### Include Everyone

## Deployment

### painless, seamless

### start small, spread out

### version control your scripts

### ability to rollback

### git, grunt, fabric

### Include Everyone

## Testing

### Keep an ear to the ground

### Watch THOSE sites

### Be a constant user

### watch your logs

### Include Everyone

## Trust

You've hopefully noticed a common thread throughout each of these. Establishing a workflow and then including everyone is important. This establishes trust within your team. This trust is important in order to maintain an overall project workflow of rapid, incremental, improvements.

### Establish a Workflow
### Include Everyone


## Wrap Up

## Fin