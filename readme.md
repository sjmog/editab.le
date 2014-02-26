# Editab.le – turn any HTML template into an editable one with CMS (and Hosting)

>logo-developer+designer high-fiving

## Developers, meet Designers (switches the two)

###Takes in any HTML and CSS files
Static mockups into fully-featured sites in minutes.
###Graphically select editable parts in the browser
Select anything in the DOM to make it editable through the CMS
###Output a fully-featured Rails app, optionally with hosting
Go local, or one-click host it with us

>Hosting has a small markup.

>Say $20 a month on Heroku and actual cost is $16 - $4 per customer

1000 customers -> $4,000 gross
$1,000 server costs
$2,000 tax
$1,000 income

## The technicalities

Based on Hackathon-Starter with Stripe SaaS subscription integrations
Node writes to a shell console on the server
Shell executes rails generate a CMS with the main index file being the uploaded file and any other attached files appropriately linked.

Users must be signed in to use the product.

Users can create a new project with a name and attached files, which are string references to an S3 bucket where uploaded files are stored and held during editing along with small files persisting the <code>names</code> and <code>values</code> arrays mentioned later, and sites, which are string references to an S3 bucket where complete Rails apps live.

The user can mark up the uploaded files in a graphical manner, a.k.a. by pointing and clicking in the browser (we're not targeting mobile here yet, but that's a possibility for the future through a tablet app etc.).

The HTML file is copied and the file copy marked up by Node so as to add an editor interface, which instructs the user to select text by highlighting it, or clicking images, etc.

Once text is highlighted, which is detected by jQuery, a toolbar appears with a name input and a button to accept.

The user gives the selected field a name for the CMS and clicks the button to commit.

A unique selector (XPath?) for the text's parent's element is found and sent to the server via AJAX with the name given in the input on the toolbar and the highlighted text or src of the image.

In the original uploaded HTML file, the element is found and the contents or src replaced by an Embedded Ruby (ERB) Rails model attribute reference, the key of which is the name submitted via AJAX, and the value of which is a string (based off an ActiveRecord text type) of the highlighted text or src also submitted via AJAX. The attribute is also added by Node to an internal array of attribute names, <code>names</code>, and the value to a different array of attribute initial values, <code>values</code>.

Node then evokes a rails generator command, which creates files among which is a model, <code>SiteContent</code>, whose attributes are each of the items in <code>names</code>, and a fixture for <code>SiteContent</code>, whose values are each of the items in <code>values</code>.

The complete Rails app is then presented to the user as a download, or immediately hostable for 14 days free, and thereafter $16 per month, with the CMS.

If the user chooses to download, they are given the Rails app free of charge as a .zip file with their name of choice.

If the user chooses hosting, Node makes a call to the Heroku API to set up a new app, committing the Rails app via Git.

The user is notified after around 30 seconds that their site is ready to go. They can add a domain if they want, otherwise it'll be the name stated at the beginning + '.herokuapp.com'

The Project is added to the list in the User profile.

In the User profile, users can cancel existing subscriptions, change passwords, close accounts, access support, add new projects, remove existing projects, access project homepages directly, access project CMSes directly, and make edits to existing projects.

When a user hovers over a project, they have the hover bar above with the option to go to the project homepage, to the CMS, or make edits.

If the user chooses to make edits, they are shown all the files in the project. Clicking a file loads it for editing. Under each file is a list of the attributes it draws from <code>SiteContent</code>, which are drawn from the files containing <code>names</code> and <code>values</code> in the same S3 bucket as the edited uploaded files. The ERB is substituted back to HTML by Node, using the <code>names</code> and <code>values</code> arrays. (Or could the static page not just be fetched from the corresponding page on the Heroku-hosted site, and the element selectors submitted earlier used to mark up editable elements with a special class, and a data-editable-name attribute?)





