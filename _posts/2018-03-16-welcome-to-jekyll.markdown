---
title: Build a Static Site w/ Jekyll
layout: post
date: '2018-03-16 16:22:31 -0600'
categories: post
---

This tutorial includes setting up a plugin for wordpress-like management of your site, installing a new theme, and deploying to netlify with a custom domain.

### Step 1 - Install Jekyll

Open your terminal and run `gem install jekyll` (may need to run `sudo gem install jekyll`)

### Step 2 - Create and run local site

Navigate to where you want your site files to be (via the terminal) and run `jekyll new <site-name>`

Then `cd` into the <site-name> folder that was just created and run `bundle exec jekyll serve` Your local site will be available at 'localhost:4000'.

### Step 3 - Install jekyll admin plugin

Open your jekyll site files with your favorite text editor. Open the file named `Gemfile` and find the part that says `group :jekyll_plugins do` you will want to add `gem 'jekyll-admin` just before the word 'end'. Make it look something like this:

```
group :jekyll_plugins do
  ... other plugins ...
  gem 'jekyll-admin'
end
```

Then run `bundle install` once that is done open your browser to [localhost:4000/admin](http://localhost:4000/admin). You can now manage your jekyll site content via this admin interface.

### Step 4 - Set up your site as a git repo

Create/login into your [github.com](https://github.com) account. Click the 'New repository' button and go through the flow to create a new repo (name your site, add a description etc).

Once you finish creating the repo you will be at a screen that looks like this: 

![fresh repo](https://user-images.githubusercontent.com/2521298/37550715-d64508da-2957-11e8-83c4-aa30e247035d.png)

We will basically be using the second option "...or push an existing repository from the command line" so leave this page open for a moment for reference.

Next open the terminal to the root of your project and run these commands:

```
git init
git add .
git commit -m "Initial commit"
```
Then you can copy the second option on the github page and just paste the two commands in:

```
git remote add origin https://github.com/<your github user>/<your repo>.git
git push -u origin master
```

Once you've done that you can refresh the github page and you will see that your jekyll site code is now available on github.

### Step 5 - Deploy to netlify

Create/login to [netlify.com](https://netlify.com).

Click the button 'New site from Git' and follow the flow to add a site from GitHub and find the repo you just created. When you select your repo there will be a button title 'Deploy site'. Just click that and you should be good to go.

When the deployment is done netlify will tell you the url where you can access the site. Go check it out, you should see your jekyll site up and running at a public netlify domain.

### Step 6 - Setup a custom domain

Within your site settings under 'Overview' click the button titled 'Domain Settings'. Click the button 'Add custom domain' and enter the domain you want the site to be hosted at.

Now we will need to get the domain to actually point to the site. I'm going to allow netlify to manage my domain. You can also do the same thing through your dns provider. To allow netlify to manage your DNS settings follow the instructions [here.](https://www.netlify.com/docs/custom-domains/?_ga=2.128801929.401463707.1521254353-1615427887.1503934537#automatic)

You will just click the little three dot icon to the right of your domain you just added and the dropdown will have an option title 'Setup netlify DNS'. Follow the instructions there (wait for dns changes to propagate) and you will be good to go!

Just one more thing you will want to do. You should allow Netlify to provide an ssl cert for your site through Lets Encrypt. Just go into the setting title 'https' and enable that setting for your domain.