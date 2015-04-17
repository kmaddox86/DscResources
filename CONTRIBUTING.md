# Contribute to DscResources repository

Hi there! We're thrilled that you'd like to contribute to this project. Your help is essential to keeping it great. 

## Use GitHub, Git, and this repository

Start by reading our [guide to getting started with GitHub](GettingStartedWithGitHub.md).

## Contributing to existing DSC resources

GitHub provides contribution model with [Pull Requests](https://help.github.com/articles/using-pull-requests/).
Once you [fork](https://help.github.com/articles/fork-a-repo/) a repository you have a full control on your fork.
To contribute changes you made back to our repository, you create a pull request.
Pull request lifecycle:

* when you create a pull request, describe what's the purpose of it in description. 
**Always create Pull Request to `dev` branch**, see [branches structure](#branches-structure) for details.
If it's relate to existing github issue, it's a good idea to put an issue reference in the description.

![Github-PR-dev.png](Images/Github-PR-dev.png)

* If it's your first contribution to DscResources, you would be asked to sign-up contributors agreement.

* CI system [runs a build with tests](#appveyor) and updates pull request status.

* One of module maintainers (it can be somebody from PowerShell team or a community member) will do a code review.

* Once code review done, merge conflicts resolved and CI build is green, maintainer will merge your changes.

### Contributing to documentation
One of the easiest ways to contribute to a PowerShell project is by helping to write and edit documentation. 
All of our documentation hosted on GitHub is written using [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown/) in the style of [this example](DscResourcesExampleHelp.md).

To [edit an existing file](https://help.github.com/articles/editing-files-in-another-user-s-repository/), simply navigate to it and click the "Edit" button. 
GitHub will automatically create your own fork of our repository where you can make your changes. 
Once you're finished, save your edits and submit a pull request to get your changes merged upstream. 

If you want to contribute new documentation, first check for [issues tagged as "Documentation"](https://github.com/PowerShell/DscResources/labels/documentation) to make sure you're not duplicating efforts.
If no one seems to be working on what you have planned:
* Open a new issue tagged as "Documentation" to tell others what you're working on
* Create a fork of our repository and start adding new Markdown-based documentation to it
* When you're ready to contribute your documentation, submit a pull request to the *dev* branch


#### Standard markdown

All of the articles in this repository use Markdown.  
While a complete introduction (and listing of all the syntax) can be found here [Markdown Home](https://help.github.com/articles/github-flavored-markdown/), the relevant basics will be covered here.

If you are looking for a good editor, try [Markdown Pad](http://markdownpad.com/).
Or use web browser: GitHub web interface provides good markdown edit expirience by itself, with syntax highlighting and Preview. 

Below is a list of the most common markdown syntax.

*   **Line breaks vs. paragraphs:** In Markdown there is no HTML `<br />` element. 
Instead, a new paragraph is designated by an empty line between two blocks of text.
Keep one line per sentence.
It will simplify diffs and history.
*   **Italics:** The HTML `<i>some text</i>` is written `*some text*`
*   **Bold:** The HTML `<strong>some text</strong>` element is written `**some text**`
*   **Headings:** HTML headings are designated by an number of `#` characters at the start of the line.  The number of `#` characters corresponds to the hierarchical level of the heading (for example, `#` = h1 and `###` = h3).
*   **Numbered lists:** To make an numbered (ordered) list start the line with `1. `.  If you want multiple elements within a single list element, format your list as follows:
        
        1.  Notice that this line is tabbed over after the '.'
        
            Now notice that there is a line break between the two paragraphs in the list element, and that the indentation here matches the indentation of the line above.

*   **Bulleted lists:** Bulleted (unordered) lists are almost identical to ordered lists except that the `1. ` is replaced with either `* `, `- `, or `+ `.  Multiple element lists work the same way as with ordered lists.
*   **Links:** The base syntax for a link is `[visible link text](link url)`.

    Links can also have references, which will be discussed in the "Link and Image References" section below.


### Improving test coverage for existing resources

All DSC modules in the DscResources should have tests written using [Pester](https://github.com/pester/Pester) included in a Tests folder. 

One of the most effective ways to report a bug is to provide a Pester test that fails. 
It dramatically simplifies work for the person who will fix it, increases code coverage, and prevents regressions in the future.

### Creating a new resource in an existing module

If you would like to add a DSC resource:
* Open an issue in the module repository where you'd like to add a DSC resource to coordinate your work with others.
* Fork the *dev* branch of the module repository you'd like to improve:
    - `git checkout dev`
    - `git checkout -b my_awesome_new_resource`
* In your own forked branch, add and develop your new resources. Make sure you:
    - Write pester tests.
    - Write documentation using GitHub Flavored Markdown 
    - Write (or alter) an example configuration in the Examples subdirectory demonstrating how your resource should be used
    - DO NOT change the *.psd1 ModuleVersion (we will be updating this before releasing to the Gallery)


## Contributing a new DSC resource module

If you would like to share your DSC resource module or create a brand new module, first [open an issue](https://github.com/PowerShell/DscResources/issues) with following information:

* What system will your DSC resources be managing?
    - For example, [xActiveDirectory](https://github.com/powershell/xActiveDirectory) models and manages Active Directory
* Will your module include [MOF-based resources](TODO) (compatible with PS/WMF 4.0 and 5.0+) or [class-based resources](TODO) (only compatible with PS/WMF 5.0+)

Next, develop your DSC resources in your own module repository. Make sure you:

* Write a set of test cases specific to your resources using Pester. Place them in a `Tests` directory.
* Use the template from the [DscResource.Template folder](DscResource.Template) as a boilerplate [appveyor.yml](appveyor.yml) for continuous integration (CI).
* Run all common tests located in [DSCResource.Tests](https://github.com/PowerShell/DscResource.Tests)

Follow up in the issue you opened to discuss repo ownership with the PowerShell team.
There are two options:
* Transfer full ownership of your module to the PowerShell organization.
This means we will have full control and permissions to the module repository.
In the future, you will have to fork and submit pull requests to commit changes as if it were any other submodule in [DscResources](https://github.com/PowerShell/DscResources).
![Transfer-Ownership](Images/GitHub-Transfer-Ownership.png)
* Allow the PowerShell organization to fork your repository and use that fork as a submodule of [DscResources](https://github.com/DscResources).
This means that you can continue to operate as you wish on your own branch of the module.
However, you should still submit pull requests to our fork in order to take your changes into the "official" version of the module. 

## AppVeyor

We use [AppVeyor](http://www.appveyor.com/) as a continious integration (CI) system.

In the `README.md` of every DSC resource module repo at the top you can see AppVeyor badge.
It indicates the last build status of master branch.
Hopefuly it's green

![AppVeyor-Badge-Green.png](Images/AppVeyor-Badge-Green.png)

This badge is **clickable**, you can open corresponding build page with logs, artifacts and tests results.
From there you can easily navigate to the whole build history.

AppVeyor builds and runs tests on every pull request and provides quick feedback about it.

![AppVeyor-Github](Images/AppVeyor-Github.png)

## Common Tests
We have provided a set of common tests for DSC resources in [DSCResource.Tests](https://github.com/PowerShell/DscResource.Tests)
They primarly concentrate on things like code style, encoding, and module version consistency.
The `appveyor.yml` file in each module repository describes the build and test sequence for CI. 
Make sure to run these tests before submitting a pull request. 

## Style guidelines

When contributing to any PowerShell repositories, please follow the following guidelines: 

* For all indentation, use 4 spaces instead of tab stops
* Make sure all files are encoding using UTF-8. 
* Windows handles [newlines](http://en.wikipedia.org/wiki/Newline) using CR+LF instead of just CR. 
For interoperability reasons, we recommend that you follow [these instructions](GettingStartedWithGitHub.md#setup-git) when installing Git on Windows so that newlines saved to GitHub are simply CRs. 
* When writing Markdown, if a paragraph includes more than one setence, end each sentence with a newline.
GitHub will still render the sentences as a single paragraph, but the readability of `git diff` will be greatly improved. 


## Branches structure

We are using a [git flow](http://nvie.com/posts/a-successful-git-branching-model/) model for development.
We recommend that you create local working branches that target a specific scope of change. 
Each branch should be limited to a single feature/bugfix both to streamline workflows and reduce the possibility of merge conflicts.
![git flow picture](http://nvie.com/img/git-model@2x.png)
