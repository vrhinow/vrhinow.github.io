+++
date = '2025-10-01T19:43:19+02:00'
draft = true
title = 'My First Post'
+++

I just started out with creating ansible modules with powershell code.
Specifically i try to provide a ansible module for a project in my
company.

As i am trying to automate Citrix Infrastructure and they just released
their REST API - which is quite buggy - i have to build a workaround in
the traditional Powershell Module they are providing.

The article however is regarding the creation of Modules inside of
vscode.

When i created my structure inside of vscode i encountered the following
error:

{% highlight %} TASK \[Create Machinecatalog\]
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
task path:
/home/username/ansible/repository/playbooks/citrix/mvd-collection-test.yml:9
Using module file
/home/username/.ansible/collections/ansible_collections/collection/citrix/plugins/modules/mvd_machinecatalog_create.ps1
Pipelining is enabled. \<hostname.corp.local\> ESTABLISH WINRM
CONNECTION FOR USER: mmvd@corp.local on PORT 5986 TO hostname.corp.local
EXEC (via pipeline wrapper) The full traceback is: The term
‘\#!powershell’ is not recognized as the name of a cmdlet, function,
script file, or operable program. Check the spelling of the name, or if
a path was included, verify that the path is correct and try again. At
line:1 char:1 + \#!powershell + \~\~\~\~\~\~\~\~\~\~\~\~~ + CategoryInfo
: ObjectNotFound: (#!powershell:String) \[\],
ParentContainsErrorRecordException + FullyQualifiedErrorId :
CommandNotFoundException

ScriptStackTrace: at <ScriptBlock>, <No file>: line 1 fatal: \[localhost
-\> hostname.corp.local\]: FAILED! =\> { “changed”: false, “msg”:
“Unhandled exception while executing module: The term ‘\#!powershell’ is
not recognized as the name of a cmdlet, function, script file, or
operable program. Check the spelling of the name, or if a path was
included, verify that the path is correct and try again.” }

PLAY RECAP
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
localhost : ok=0 changed=0 unreachable=0 failed=1 skipped=0 rescued=0
ignored=0  
{% endhighlight %}

<figure>
<img src="./d5fdfd1033f93b02d216fc1f70e2c5da.png"
alt="d5fdfd1033f93b02d216fc1f70e2c5da.png" />
<figcaption
aria-hidden="true">d5fdfd1033f93b02d216fc1f70e2c5da.png</figcaption>
</figure>

I tried to troubleshoot the isse but couldn‘t seem to figure it out. A
collegue of mine pointed out that the file encoding seems of.

In the bottom right corner it‘s **UTF8-BOM**. This is an issue for linux
systems but standard for Windows. This is an issue because the code will
be base64ed before transferring to the target system. The UTF8-BOM
messes up the characters and we get these types of issues.

<figure>
<img src="./0bba72f9f6d66422a60ba081af167e06.png"
alt="0bba72f9f6d66422a60ba081af167e06.png" />
<figcaption
aria-hidden="true">0bba72f9f6d66422a60ba081af167e06.png</figcaption>
</figure>

We can Click on the Encoding and Save the File in new Encoding and
select „UTF8“ from the command palette which is standard for Linux
systems.

Afterwards i set the default for my VSCode to UTF8 via the
Files.Encoding Setting.
