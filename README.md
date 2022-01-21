This is not live yet.
To look at the website:
* check it out locally: git clone https://github.com/apache/db-site.git
* run `mvn clean compile`
* in your checked out workspace, open the file `db-site\target\site\index.html` in your favorite web browser.

# TODO
* Fix .htaccess -> `RewriteBase`
* Fix .asf.yaml.publish -> `subdir`
* Fix .asf.yaml -> `notifications`
* Enable/use Actions
  * Recreate-site-branch
* Anything else?
* 
* Proof reading


# Apache DB Website

This repository contains the sources for the [Apache DB website](https://db.apache.org/).

## Building the Site

The content and styling of the site is defined in the [AsciiDoc](https://asciidoc.org/) format.
It is built using [Maven](https://maven.apache.org/).
For details on publishing the site see section [Publishing the Site](#publishing-the-site).

The site can be built by calling `mvn clean compile`. This generates the HTML files in `target/site`.
Most of the site will work with the exception of the javadoc file downloads.
If needed, call `mvn package`. This copies the javadoc files to `target/site`.
The site can then be viewed by opening the local file `target/site/index.html` in a browser.

## Contributing to the Site

Contributions to the website are always appreciated.
If you are new to this project, please have a look at our [mailing losts](https://db.apache.org/mail.html) page first.

This repository contains the Apache DB website source.

* The AsciiDoc sources can be found in `src/main/asciidoc`.
* The website menu is defined in `src/main/template`.
* Additional pre-compiled resources are located in `src/main/resources`.

Contributions to this repository follow the default [GitHub workflow](https://guides.github.com/introduction/flow/)
using [forks](https://guides.github.com/activities/forking/).

To contribute changes, you can follow these steps:

* Adapt the AsciiDoc files in `src/main/asciidoc` or the website menu in  `src/main/template`.
* Build the site (see [above](#building-the-site)) and verify the generated website by viewing `target/site/index.html` locally with a web browser.
* Commit the source changes (not the build artifacts) in your branch and open a pull request.

### Reporting issues
If you find any issues please provide a PR or [create a JIRA ticket](https://issues.apache.org/jira/projects/JDO/issues/?filter=allopenissues).

### Publishing the Site
After changes have been made to the sources in the `src/main/asciidoc` or `src/main/template` directory, changes will be published automatically to the live web site by simply pushing changes to the main branch of the repository. The process is as follows:

1. Pushing changes to the main branch invokes the post-push script in [`db-site/.github/workflows/deploy-site.yml`](./.github/workflows/deploy-site.yml) which builds the site in `target/site` via `mvn clean package`.

2. If the build is successful, the build artifacts in the main branch are pushed to the `publish` branch.

3. Once the changes have been pushed to the `publish` branch, the script in `.asf.yaml.publish` is automatically invoked. This script is executed by Apache Infrastructure machines, and it publishes changes to `db.apache.org/`. It may take some time for the changes to be seen on the live site.
   Details on the use of .asf.yaml is found [here](https://cwiki.apache.org/confluence/display/INFRA/git+-+.asf.yaml+features#git.asf.yamlfeatures-WebSiteDeploymentServiceforGitRepositories).
