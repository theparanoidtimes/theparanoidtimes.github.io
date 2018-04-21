---
layout: page
title: tabellarium
category: projects
project-repo: https://github.com/theparanoidtimes/tabellarium
permalink: /:categories/:title
---

*tabellarium* is a library that provides the means to execute tasks against
e-mail messages in one folder in the e-mail mailbox. Those tasks can be anything
from reading and processing e-mails, saving them to a offline resource to
modifying some state on the server. The library only works with IMAP mailboxes
and only in one folder at the time. But multiple instances can work with multiple
folders as long as they are not the same.

Main behavior is defined in the `MailboxTaskExecutor` interface.
It's only implementation is `ImapMailboxFolderTaskExecutor` that works with IMAP
mailboxes. You can instantiate it like this:
```java
MailboxTaskExecutor executor =
    new ImapMailboxFolderTaskExecutor
    ("hostAddress", "username", "password", "Inbox");
```
The constructor arguments are self-explanatory. `ImapMailboxFolderTaskExecutor`
has some other settings like port number, 'should use IMAPS' and such. Besides
them there are 3 things that should require some attention. In code:
```java
// after doing something with an e-mail message
// mark it for deletion
executor.setDeleteAfterRetrieval(false);

// consider seen e-mails when executing tasks
executor.setRetrieveSeenEmails(true);

// Batch size means that 100 e-mail messages will be retrieved
// when executing tasks. If there are less than 100 then all
// will be retrieved. If batch size is 0 than all e-mails
// will be considered.
executor.setBatchSize(100);
```

How *tabellarium* actually works? Again in code:
```java
executor.executeForEachEmail(message -> {
    // do something with the e-mail message...
});
```
This will connect to the mailbox with information from the constructor arguments
and execute the task defined against each e-mail message. The settings defined before
also come into play here.

If any exception occurs during the task execution the executor will try to revert
the status flags if they are changed - specifically revert *SEEN* and *DELETED*.

There are some built in tasks - email handlers because they implement the
`EmailHandler` interface - in the library that provide some basic
functionalities. One of them is:
```java
executor.executeForEachEmail(
    new ChangeMessageFlagEmailHandler("deleted", true));
```
This will set the 'deleted' flag to true for each mail, essentially deleting them
on the server. In order for this to work (this and any task that modifies
state on the server) an active session must be maintained while executing the
task. This is the default behavior when providing the `EmailHandler` instance
to the executor. But if you want to do something with the text of the e-mail,
for example writing it to a file, you will need to force the retrieval of the
body from the server. To do this provide an instance of the
`UnlinkedEmailHandler` class to the executor.

Implementations provided in the library are `PrintingEmailHandler` and
`PrintInFileEmailHandler` that write the whole e-mail in provided stream and
in file, respectfully.
```java
executor.executeForEachEmail(new PrintingEmailHandler(System.out));

executor.executeForEachEmail(
    new PrintInFileEmailHandler("file name"));
```

Two other methods are defined in the API:
```java
// This will retrieve the copy of the messages from the mailbox.
// It will honor the settings defined above.
List<Message> messages = executor.retrieveEmails();

// This will return true if there are e-mails in the mailbox.
// Unlike the other methods it honors only
// setRetrieveSeenEmails flag.
boolean result = executor.areThereRemainingEmails();
```
These can possibly be just another tasks that are passed to the
`executeForEachEmail` method and probably will be refactored in that manner
in the future, but for now they are separate methods.

Check out the [repo]({{ page.project-repo }}) for source.
