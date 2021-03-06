[Prev](cgis.md) ![Icinga](../images/logofullsize.png "Icinga") [Next](cgiparams.md)

* * * * *

6.2. Authentication And Authorization In The Classic UI
-------------------------------------------------------

6.2.1. [Introduction](cgiauth.md#introduction_cgiauth)

6.2.2. [Definitions](cgiauth.md#definitionscgiauth)

6.2.3. [Setting Up Authenticated Users](cgiauth.md#configwebusers)

6.2.4. [Enabling Authentication/Authorization Functionality In The
Classic UI](cgiauth.md#enablecgiauth)

6.2.5. [Default Permissions To Classic UI
Information](cgiauth.md#defaultpermissions)

6.2.6. [Granting Additional Permissions To Classic UI
Information](cgiauth.md#additionalpermissions)

6.2.7. [Classic UI Authorization
Requirements](cgiauth.md#requirementscgiauth)

6.2.8. [Authentication On Secured Web
Servers](cgiauth.md#securedwebservers)

### 6.2.1. Introduction

This documentation describes how the Icinga Classic UI (formerly called
"CGI") decides who has access to view monitoring and configuration
information, and who can submit commands to the Icinga daemon through
the Classic web interface.

### 6.2.2. Definitions

Before continuing, it is important that you understand the meaning of
and difference between authenticated users and authenticated contacts:



### 6.2.3. Setting Up Authenticated Users

Assuming you configured your web server as described in the [quickstart
guide](quickstart.md "2.3. Quickstart Installation Guides"), it should
require that you authenticate before accessing the Icinga Classic UI.
You should also have one user account (*icingaadmin*) that can access
the Classic UI.

As you define more
[contacts](objectdefinitions.md#objectdefinitions-contact) for
receiving host and service notifications, you'll most likely want to let
them access the Icinga web interface. You can use the following command
to add additional users who can authenticate to the UI. Replace
\<username\> with the actual username you want to add. In most cases,
the username should match the short name of a
[contact](objectdefinitions.md#objectdefinitions-contact) that has
been defined.

</code></pre> 
 htpasswd /usr/local/icinga/etc/htpasswd.users <username>
</code></pre>

### 6.2.4. Enabling Authentication/Authorization Functionality In The Classic UI

The next thing you need to do is make sure that the Classic UI is
configured to use the authentication and authorization functionality in
determining what information and/or commands users have access to. This
is done be setting the
[use\_authentication](configcgi.md#configcgi-use_authentication)
variable in the [Classic UI configuration
file](configcgi.md "3.6. CGI Configuration File Options") to a
non-zero value. Example:

<pre><code>
 use_authentication=1
</code></pre>

Okay, you're now done with setting up basic authentication/authorization
functionality in the Classic UI.

### 6.2.5. Default Permissions To Classic UI Information

So what default permissions do users have in the Classic UI by default
when the authentication/authorization functionality is enabled?

Classic UI Data

Authenticated
Contacts^[\*](cgiauth.md#definitionscgiauth "6.2.2. Definitions")^

Other Authenticated
Users^[\*](cgiauth.md#definitionscgiauth "6.2.2. Definitions")^

Host Status Information

Yes

No

Host Configuration Information

Yes

No

Host History

Yes

No

Host Notifications

Yes

No

Host Commands

Yes

No

Service Status Information

Yes

No

Service Configuration Information

Yes

No

Service History

Yes

No

Service Notifications

Yes

No

Service Commands

Yes

No

All Configuration Information

No

No

System/Process Information

No

No

System/Process Commands

No

No

*Authenticated
contacts^[\*](cgiauth.md#definitionscgiauth "6.2.2. Definitions")^*
are granted the following permissions for each **service** for which
they are contacts (but not for services for which they are not
contacts)...





*Authenticated
contacts^[\*](cgiauth.md#definitionscgiauth "6.2.2. Definitions")^*
are granted the following permissions for each **host** for which they
are contacts (but not for hosts for which they are not contacts)...









It is important to note that by default **no one** is authorized for the
following...





You will undoubtably want to access this information, so you'll have to
assign additional rights for yourself (and possibly other users) as
described below...

### 6.2.6. Granting Additional Permissions To Classic UI Information

You can grant *authenticated contacts* or other *authenticated users*
permission to additional information in the Classic UI by adding them to
various authorization variables in the [Classic UI configuration
file](configcgi.md "3.6. CGI Configuration File Options"). We realize
that the available options don't allow for getting really specific about
particular permissions, but its better than nothing..

Additional authorization can be given to users by adding them to the
following variables in the Classic UI configuration file...








### 6.2.7. Classic UI Authorization Requirements

If you are confused about the authorization needed to access various
information in the Classic UI, read the ***Authorization Requirements***
section for each form as described
[here](cgis.md "6.1. Icinga Classic UI: Information On The Modules").

### 6.2.8. Authentication On Secured Web Servers

If your web server is located in a secure domain (i.e., behind a
firewall) or if you are using SSL, you can define a default username
that can be used to access the Classic UI. This is done by defining the
[default\_user\_name](configcgi.md#configcgi-default_user_name) option
in the [Classic UI configuration
file](configcgi.md "3.6. CGI Configuration File Options"). By defining
a default username that can access the Classic UI, you can allow users
to access the Classic UI without necessarily having to authenticate to
the web server. You may want to use this to avoid having to use basic
web authentication, as basic authentication transmits passwords in clear
text over the Internet.

**Important:** Do *not* define a default username unless you are running
a secure web server and are sure that everyone who has access to the
Classic UI has been authenticated in some manner. If you define this
variable, anyone who has not authenticated to the web server will
inherit all rights you assign to this user!

* * * * *

[Prev](cgis.md) | [Up](ch06.md) | [Next](cgiparams.md)

6.1. Icinga Classic UI: Information On The Modules  |<=== [Index](index.md) ===>|  6.3. Information On Classic UI parameters

© 1999-2009 Ethan Galstad, 2009-2015 Icinga Development Team,
http://www.icinga.org
