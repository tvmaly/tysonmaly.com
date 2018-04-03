---
author: admintm
categories:
- postgresql
- osx
date: "2017-04-21T02:37:55Z"
guid: http://www.tysonmaly.com/?p=214
id: 214
title: How to remove an old version of postgresql from OSX with multiple versions
  installed
url: /postgresql/remove-old-version-postgresql-osx/
---

Here is a short tutorial on how to remove older versions of PostgreSQL database from OSX when you have multiple versions installed.

If you follow one of the popular answers on StackOverFlow you may accidentally delete an important file for your other newer versions of PostgreSQL running on your Mac.  These instructions assume you installed the database with the EnterpriseDB installer.

Here are the steps you need to follow:

  1. First, make a backup of the database if you need any data or schema. Use the graphical PgAdmin or commandline to do this.
  2. Open a terminal window
  3. Change to the super user by typing sudo su in that terminal window, enter your password
  4. Change directory to <pre class="lang-sql prettyprint prettyprinted"><code>&lt;span class="pun">/&lt;/span>&lt;span class="pln">Library&lt;/span>&lt;span class="pun">/&lt;/span>&lt;span class="pln">PostgreSQL&lt;/span>&lt;span class="pun">/&lt;/span>&lt;span class="lit">X.Y&lt;/span>&lt;span class="pun">/&lt;/span>&lt;span class="pln">uninstall-postgresql&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">app&lt;/span>&lt;span class="pun">/&lt;/span>&lt;span class="pln">Contents&lt;/span>&lt;span class="pun">/&lt;/span>&lt;span class="pln">MacOS&lt;/span>&lt;span class="pun">/&lt;/span></code></pre>
    
    Where X.Y is the older version you want to remove, example 9.5</li> 
    
      * run the script in that directory <pre class="lang-sql prettyprint prettyprinted"><code>&lt;span class="pln">./installbuilder&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">sh&lt;/span></code></pre>
        
        <pre class="lang-sql prettyprint prettyprinted"><code>&lt;span class="pln">This should remove all of the main files but may not remove data files.&lt;/span></code></pre>
    
      * Multiple versions of PostgreSQL on the same machine will share the file <pre class="lang-sql prettyprint prettyprinted"><code>&lt;span class="pun">/&lt;/span>&lt;span class="pln">etc&lt;/span>&lt;span class="pun">/&lt;/span>&lt;span class="pln">postgres-reg&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">ini&lt;/span></code></pre>
        
        Make sure not to delete it.  Edit it and remove the section for the older version you want to remove from your machine.</li> 
        
          * Next remove the directory version specific directory and any files under it
  
            `<span class="pun">/</span><span class="pln">Library</span><span class="pun">/</span><span class="pln">PostgreSQL</span><span class="pun">/</span><span class="lit">X.Y</span>`</ol> 
        
        <p class="lang-sql prettyprint prettyprinted">
          example rm -rf /Library/PostgreSQL/9.5
        </p>
        
        <p class="lang-sql prettyprint prettyprinted">
          8. Finally, you need to update the home directory of the postgres user to point to the new directory of the new version of the database /Library/PostgreSQL/9.6
        </p>
        
        <p class="lang-sql prettyprint prettyprinted">
          Open up a terminal window and run
        </p>
        
        <p class="lang-sql prettyprint prettyprinted">
          open &#8220;/System/Library/CoreServices/Applications/Directory Utility.app&#8221;
        </p>
        
        <p class="lang-sql prettyprint prettyprinted">
          click the &#8220;Directory Editor&#8221; icon at the top of the app.
        </p>
        
        <p class="lang-sql prettyprint prettyprinted">
          click on the lock to authenticate yourself.  enter your main user and password.  The lock icon will turn to unlock if you did it correctly.
        </p>
        
        <p class="lang-sql prettyprint prettyprinted">
          next make sure the drop down &#8220;Viewing&#8221; has the value Users selected.  Locate the PostgreSQL entry in the list on the left by scrolling down and next select it.   Now choose the NFSHomeDirectory on the right side panel.  Change the 9.5 value to 9.6 in the string below.  Then click the Save button.  Now quit out of the application.
        </p>
        
        That is it, if you completed those steps, you will have removed the older version of the database.
