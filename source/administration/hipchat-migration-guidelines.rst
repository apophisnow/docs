Migrating from HipChat to Mattermost
=====================================

You can migrate HipChat users and message histories to Mattermost using the following guidelines.

Step 1:  Set up your Mattermost Instance
-----------------------------------------
- `Go to Mattermost download page <https://about.mattermost.com/download/>`_ to install Mattermost in your environment using one of the installation guides for Linux binary install, Docker install or various orchestrated installations. 

Questions? Please visit our `troubleshooting forum <https://forum.mattermost.org/t/how-to-use-the-troubleshooting-forum/150>`_ for help. 

Step 2:  Export your data from HipChat Data Center or HipChat Server
------------------------------------------------------------------------

HipChat Server / HipChat Data Server:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you’re able to upgrade HipChat Server or HipChat Data Center to the latest version, we recommend using Group Export Dashboard to export your data. If you’re unable to upgrade, see Command Line Interface procedure below. 

*Using the Group Export Dashboard:*

#. Log in to your Hipchat Server (e.g. hipchat.yourcompany.com).
#. Click on **Server Admin > Export**.
#. Select the data to export.
#. In the **Password** and **Confirm Password** fields, create a password to protect your archive files (Store this password as it is not saved anywhere else).
#. Click **Export**. Once the export is done, you will receive an email with a link to download the file.

*If you’re unable to use the Group Export Dashboard, use the Command Line Interface to export:*

#. Go to **CLI**.
#. Enter ``hipchat export --export  -p your_password``.
#. Once the export is done, you will receive an email with a link to download the file.

More detailed instructions can be found at https://confluence.atlassian.com/hipchatdc3/export-data-from-hipchat-data-center-913476832.html.


Step 3: Import your data into Mattermost 
----------------------------------------

1. Follow the `Mattermost Bulk Load Tool <https://docs.mattermost.com/deployment/bulk-loading.html>`_ guide to import your data into Mattermost. 

  - Note: Efforts are underway to source scripts from the Mattermost community to further automate this step. If you’re interested in contributing, please let us know at info@mattermost.com, Twitter or Mattermost forums at https://forum.mattermost.org.

2. Alternatively, `contact Mattermost <https://mattermost.com/contact-us/>`_ for partner recommendations for your region to assist in your import. 
  
Step 4: Onboard your users into Mattermost
---------------------------------------------
After importing users, you can send out an announcement via email or via your old system (or both) to let users know how to log into Mattermost with their old accounts or how to create new accounts.
 
**Announcing Mattermost onboarding in your previous messaging system:**
 
Use the following message template to alert users of the migration::

     @all, we’re moving communications to a new Mattermost server. You can start your new account by going to the [your new     location, e.g. ``https://yourcompany.com/mattermost``], clicking on **I forgot my password** and entering the email you     used on this system in the Reset Password page to set up new credentials. Your message history and channels should carry     over from this system into Mattermost. Any questions? Please let us know.

**Announcing Mattermost onboarding using email using username/password:**

#. Get a list of email addresses of people in the new system by running a database query on Mattermost. Run ``SELECT Email FROM Users`` from either MySQL or PostgreSQL databases. 
#. Adapt the `migration announcement email template <https://docs.mattermost.com/administration/migration-announcement-email-template.html>`_ to let users know how to reclaim their old accounts or start new ones.

Onboard users using SSO in Mattermost
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Alternatively, you can choose to set up SSO (Single Sign-on) with Mattermost if you are using an Enterprise version.  

#. Configure `Active Directory/LDAP <https://docs.mattermost.com/deployment/sso-ldap.html>`_ or `SAML Single Sign-on <https://docs.mattermost.com/deployment/sso-saml.html>`_ from the **System Console**.
#. Adjust the messaging templates above to remove "password reset" references and indicate which SSO system credentials Mattermost has configured.
