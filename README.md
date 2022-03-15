# D-Bus - the mini README

Or: get in touch with a secret service.

## What is D-Bus?

D-Bus is to communicate with the system or applications. Said that...

## How to communicate? (applications only here)

Although the whole thing comes with the term "Bus" in, the Bus is not involved
here, as the following examples are all a one-to-one communication. (Strictly
viewed, the communication still goes 'through' the bus, so speaking technically
this is incorrect, but from a user perspective you don't have to care of)

Applications offer their abilities via so called "Services", "Pathes" (to
"Objects") and "Interfaces". Interfaces offer "Properties" to read and "Methods"
to invoke (i.e. execute, also: "trigger" or "call").

## Stepping into...

### Services

Most applications offer many so called Services. You might think of this as the
plate on a door of a room, you go through and enter a worlds of Objects (in 
cabinets) and their Interfaces . These Interfaces have Properties and Methods
(buttons to push and displays to read).

*Note: Service names are mainly made of characters, digits and dots (!).*

Services are tight to their creating process. So some Appplications might offer
there (basic) Service name extended by a dash and their process id. (Process
ids might be obtaines with pgrep(1).)

### Object (Pathes)

Objects offer Interfaces.

Objects pathes are mainly made of characters, digits, underscores and slashes (!).
(See the distinction to the naming of Services, that uses dots as delimizers).
So basicly Object Pathes resemble Linux filesystem pathes, as they always start
with a slash ('/').

### Interfaces

Interfaces have Properties to read and Methods to execute. Methods can require
Parameters. Parameters often are simple boolean values.

When using these, the Interface and Property or Method name have to be used in
junction. The junction is a single dot.

### Properties and Methods

Properties and Methods resemble the dot notation, that Services do. They actualy
might even copy the containing Service Name into it. This is particulary confusing
to everyone new to D-Bus.

### Interfaces,  Properties and Methods

Interfaces, Properties and Methods always have to be used in junction. When it
comes to adress these, the junction is a single dot between these. The Property
or Method name is always a single word.

Hint: If the Property or Method is unique within the Object, the Interface part
may be ommittted in the commands below.

### Command Line Pgrograms

Command line programs play around with the above introduced terms.

#### qdbus(1)

qdbus(1) is kind of a simple command to use. The very basic usage is:

```
# reading a property:
$ qdbus <service> <object> <interface>.<property>

# execute a simple method:
$ qdbus <service> <object> <interface>.<method>

# execute a method with parameters:
$ qdbus <service> <object> <interface>.<method> <param> [<param>]

```

#### dbus-send(1)

```
# reading a property:
$ dbus-send --print-reply --dest=<service> <object> \
	org.freedesktop.DBus.Properties.Get \
	string:<interface> \
	string:<property>

# execute a simple method (without params):
$ dbus-send --type=method_call --dest=<service> <object> \
	<interface>.<method>

# execute a method (with params):
$ dbus-send --type=method_call --dest=<service> <object> \
	<interface>.<method> \
	string:<param> [string:<param>]
```

Conclusion: when it comes to methods with parameters or ereading properties,
things get realy dirty with dbus-send(1).


### Graphical Assistance

There are couple of GUI applications, that help more or less the curios user
or developer to step into the world.

The first recommendation is Gnomes "D-Feet", that clearly identfy the things
with their given term.


#### Gnome D-Feet

Quite nice and usefull.


#### Qt QDBusViewer

If you are starting with D-Bus, avoid that one. The biggest fail here is that
it mixes objects, interfaces in a common tree explorer style. Absolutly
confusing, if you try to learn on d-bus.


#### Bustle

Quite a complex tool, more oriented on monitoring and even debugging. Likely not
for starters as well.
