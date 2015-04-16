Disqus integration for TYPO3 Neos
=================================

This is a TYPO3 Neos plugin that integrates Disqus discussions into your site
(in case you're -- like me -- too lazy to implement your own commenting system
in Neos).

Setup
-----

### Requirements

Tested with TYPO3 Neos 1.2. Should work with other releases too, though.

### Installation

Composer. Easy.

    composer require helmich/disqus

Integration as individual content element
-----------------------------------------

You can insert a Disqus discussion as an individual content element. It is
listed under "Plugins" when inserting a new content element.

The "comment" content element is not inline-editable. There are two options
you can change using the inspector, though:

* **Site name**. This is your short site name under which your site is
  registered at Disqus. When including more discussion elements, it might be a
  good idea to leave this empty and set this value via TypoScript (see below for
  that).

* **Thread identifier**. The identifier that is used for the comment thread.
  When left empty, the node identifier of the nearest document node will be
  used as a discussion identifier (which is a quite sensible default that should
  work in most cases).

When integrating more than a few discussions, it will become tedious to
configure your site name for each one individually. You can override the site
name using TypoScript:

    page {
        prototype(Helmich.Disqus:Discussion) {
            shortname = 'your-site-name'
        }
    }

Integration Disqus on all pages
-------------------------------

You can use this plugin to integrate Disqus discussions on all (or a subset) of
all pages using TypoScript:

    page = TYPO3.Neos:Page {
        // Other definitions...

        body {
            parts {
                discussion = Helmich.Disqus:Discussion {
                    // Override template if necessary:
                    // templatePath = '...'

                    // Override site name if necessary:
                    // shortname = 'your-site-name'
                }
            }
        }
    }

Inside your page fluid template, then simply render the content element:

    {parts.discussion -> f:format.raw()}