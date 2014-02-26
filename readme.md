## Editab.le – turn any HTML template into an editable one with CMS (and Hosting)
_____

>logo-developer+designer high-fiving

# Developers, meet Designers (switches the two)

#Takes in any HTML and CSS files
Static mockups into fully-featured sites in minutes.
#Graphically select editable parts in the browser
Select anything in the DOM to make it editable through the CMS
#Output a fully-featured Rails app, optionally with hosting
Go local, or one-click host it with us

>Hosting has a small markup.

>Say $20 a month on Heroku and actual cost is $16 - $4 per customer

1000 customers -> $4,000 gross
$1,000 server costs
$2,000 tax
$1,000 income

____
## The technicalities

Based on Hackathon-Starter with Stripe SaaS subscription integrations
Node writes to a shell console on the server
Shell executes rails generate a CMS with the main index file being the uploaded file and any other attached files appropriately linked.

The user can mark up the uploaded files in a graphical manner, a.k.a. by pointing and clicking in the browser (we're not targeting mobile here yet, but that's a possibility for the future through a tablet app etc.).

The HTML file is copied and the file copy marked up by Node so as to add an editor interface, which instructs the user to select text by highlighting it, or clicking images, etc.

Once text is highlighted, which is detected by jQuery, a toolbar appears with a name input and a button to accept.

The user gives the selected field a name for the CMS and clicks the button to commit.

A unique selector (XPath?) for the text's parent's element is found and sent to the server via AJAX with the name given in the input on the toolbar and the highlighted text or src of the image.

In the original uploaded HTML file, the element is found and the contents or src replaced by an Embedded Ruby (ERB) Rails model attribute reference, the key of which is the name submitted via AJAX, and the value of which is a string (based off an ActiveRecord text type) of the highlighted text or src also submitted via AJAX. The attribute is also added by Node to an internal array of attribute names, <code>names</code>, and the value to a different array of attribute initial values, <b>values</b>.

Node then evokes a rails generator command, which creates files among which is a model, <code>SiteContent</code>, whose attributes are each of the items in <code>names</code>, and a fixture for <code>SiteContent</code>, whose values are each of the items in <code>values</code>.





